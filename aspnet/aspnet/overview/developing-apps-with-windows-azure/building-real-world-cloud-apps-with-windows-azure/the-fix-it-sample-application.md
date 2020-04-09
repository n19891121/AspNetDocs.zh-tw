---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: '附錄: 修復它範例應用程式(使用 Azure 構建真實世界的雲端應用程式) |微軟文件'
author: MikeWasson
description: 使用 Azure 電子書建構真實世界雲端應用基於 Scott Guthrie 開發的演示文稿。 它解釋了13種模式和做法,他可以...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: 896196bdb6a6b0d12a6c798ead510e37dd38a9fc
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675989"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="8e9ef-104">附錄:修復它範例應用程式(使用 Azure 建構真實世界的雲端應用程式)</span><span class="sxs-lookup"><span data-stu-id="8e9ef-104">Appendix: The Fix It Sample Application (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="8e9ef-105">由[邁克·瓦森](https://github.com/MikeWasson),[里克·安德森](https://twitter.com/RickAndMSFT),[湯姆·戴克斯特拉](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8e9ef-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="8e9ef-106">下載修復項目</span><span class="sxs-lookup"><span data-stu-id="8e9ef-106">Download The Fix It Project</span></span>](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> <span data-ttu-id="8e9ef-107">使用 Azure 電子書**建構真實世界雲端應用**基於 Scott Guthrie 開發的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="8e9ef-108">它解釋了 13 種模式和做法,這些模式和做法可以説明您成功開發雲端的 Web 應用。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="8e9ef-109">有關電子書的資訊,請參閱[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="8e9ef-110">使用 Azure 電子書建構真實世界雲端應用的此附錄包含以下部分,這些部分提供有關「修復它」範例應用程式的其他資訊,您可以下載:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-110">This appendix to the Building Real World Cloud Apps with Azure e-book contains the following sections that provide additional information about the Fix It sample application that you can download:</span></span>

- [<span data-ttu-id="8e9ef-111">已知問題</span><span class="sxs-lookup"><span data-stu-id="8e9ef-111">Known issues</span></span>](#knownissues)
- [<span data-ttu-id="8e9ef-112">最佳作法</span><span class="sxs-lookup"><span data-stu-id="8e9ef-112">Best practices</span></span>](#bestpractices)
- [<span data-ttu-id="8e9ef-113">如何從本地電腦上的 Visual Studio 執行應用</span><span class="sxs-lookup"><span data-stu-id="8e9ef-113">How to run the app from Visual Studio on your local computer</span></span>](#run-in-vs)
- [<span data-ttu-id="8e9ef-114">如何使用 Windows PowerShell 文稿將基本應用部署到 Azure 應用服務 Web 應用</span><span class="sxs-lookup"><span data-stu-id="8e9ef-114">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>](#deploybase)
- [<span data-ttu-id="8e9ef-115">對 Windows 電源外殼文稿進行故障排除</span><span class="sxs-lookup"><span data-stu-id="8e9ef-115">Troubleshooting the Windows PowerShell scripts</span></span>](#troubleshooting)
- [<span data-ttu-id="8e9ef-116">如何將具有佇列處理的應用部署到 Azure 應用服務 Web 應用和 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="8e9ef-116">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a><span data-ttu-id="8e9ef-117">已知問題</span><span class="sxs-lookup"><span data-stu-id="8e9ef-117">Known issues</span></span>

<span data-ttu-id="8e9ef-118">Fix It 應用程式最初是為了盡可能簡單地說明本電子書中介紹的一些模式而開發的。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-118">The Fix It app was originally developed in order to illustrate as simply as possible some of the patterns presented in this e-book.</span></span> <span data-ttu-id="8e9ef-119">但是,由於電子書是關於構建真實世界的應用程式,因此我們進行了修復 It 代碼的審核和測試過程,類似於我們為發佈軟體所做的操作。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-119">However, since the e-book is about building real-world apps, we subjected the Fix It code to a review and testing process similar to what we'd do for released software.</span></span> <span data-ttu-id="8e9ef-120">我們發現了一些問題,與任何實際應用程式一樣,我們修復了其中一些問題,其中一些問題被推遲到以後的版本中。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-120">We found a number of issues, and as with any real-world application, some of them we fixed and some of them we deferred to a later release.</span></span>

<span data-ttu-id="8e9ef-121">以下清單包括應在生產應用程式中解決的問題,但由於以下原因,我們決定在 Fix It 範例應用程式的初始版本中不解決。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-121">The following list includes issues that should be addressed in a production application, but for one reason or another we decided not to address in the initial release of the Fix It sample application.</span></span>

### <a name="security"></a><span data-ttu-id="8e9ef-122">安全性</span><span class="sxs-lookup"><span data-stu-id="8e9ef-122">Security</span></span>

- <span data-ttu-id="8e9ef-123">確保無法將任務分配給不存在的擁有者。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-123">Ensure that you can't assign a task to a non-existent owner.</span></span>
- <span data-ttu-id="8e9ef-124">確保只能查看和修改您創建或分配給您的任務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-124">Ensure that you can only view and modify tasks that you created or are assigned to you.</span></span>
- <span data-ttu-id="8e9ef-125">將 HTTPS 用於登錄頁面和身份驗證 Cookie。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-125">Use HTTPS for sign-in pages and authentication cookies.</span></span>
- <span data-ttu-id="8e9ef-126">指定身份驗證 Cookie 的時間限制。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-126">Specify a time limit for authentication cookies.</span></span>

### <a name="input-validation"></a><span data-ttu-id="8e9ef-127">輸入驗證</span><span class="sxs-lookup"><span data-stu-id="8e9ef-127">Input validation</span></span>

<span data-ttu-id="8e9ef-128">通常,生產應用執行比修復它應用更多的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-128">In general, a production app would do more input validation than the Fix It app.</span></span> <span data-ttu-id="8e9ef-129">例如,允許上載的圖像大小/圖像檔大小應加以限制。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-129">For example, the image size / image file size allowed for upload should be limited.</span></span>

### <a name="administrator-functionality"></a><span data-ttu-id="8e9ef-130">管理員功能</span><span class="sxs-lookup"><span data-stu-id="8e9ef-130">Administrator functionality</span></span>

<span data-ttu-id="8e9ef-131">管理員應該能夠更改現有任務的擁有權。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-131">An administrator should be able to change ownership on existing tasks.</span></span> <span data-ttu-id="8e9ef-132">例如,任務的建立者可能會離開公司,除非啟用了管理訪問,否則任何人都無權維護該任務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-132">For example, the creator of a task might leave the company, leaving no one with authority to maintain the task unless administrative access is enabled.</span></span>

### <a name="queue-message-processing"></a><span data-ttu-id="8e9ef-133">佇列訊息處理</span><span class="sxs-lookup"><span data-stu-id="8e9ef-133">Queue message processing</span></span>

<span data-ttu-id="8e9ef-134">修復 It 應用中的佇列消息處理設計為簡單,以便用最少的代碼來說明以隊列為中心的工作模式。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-134">Queue message processing in the Fix It app was designed to be simple in order to illustrate the queue-centric work pattern with a minimum amount of code.</span></span> <span data-ttu-id="8e9ef-135">此簡單代碼不足以用於實際生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-135">This simple code would not be adequate for an actual production application.</span></span>

- <span data-ttu-id="8e9ef-136">該代碼不保證最多處理一次每個佇列消息。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-136">The code does not guarantee that each queue message will be processed at most once.</span></span> <span data-ttu-id="8e9ef-137">當您從佇列中收到消息時,有一個超時期間,在此期間消息對其他佇列偵聽器不可見。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-137">When you get a message from the queue, there is a timeout period, during which the message is invisible to other queue listeners.</span></span> <span data-ttu-id="8e9ef-138">如果超時在刪除郵件之前過期,則消息將再次可見。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-138">If the timeout expires before the message is deleted, the message becomes visible again.</span></span> <span data-ttu-id="8e9ef-139">因此,如果輔助角色實例花費很長時間來處理消息,則從理論上講,同一消息可以處理兩次,從而導致資料庫中出現重複的任務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-139">Therefore, if a worker role instance spends a long time processing a message, it is theoretically possible for the same message to get processed twice, resulting in a duplicate task in the database.</span></span> <span data-ttu-id="8e9ef-140">有關此問題的詳細資訊,請參閱[使用 Azure 儲存佇列](https://msdn.microsoft.com/library/ff803365.aspx#sec7)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-140">For more information about this issue, see [Using Azure Storage Queues](https://msdn.microsoft.com/library/ff803365.aspx#sec7).</span></span>
- <span data-ttu-id="8e9ef-141">通過批處理消息檢索,佇列輪詢邏輯可能更具成本效益。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-141">The queue polling logic could be more cost-effective, by batching message retrieval.</span></span> <span data-ttu-id="8e9ef-142">每次調用[CloudQueue.GetMessageasync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx)時,都會有一個交易成本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-142">Every time you call [CloudQueue.GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), there is a transaction cost.</span></span> <span data-ttu-id="8e9ef-143">相反,您可以調用[CloudQueue.GetMessagesAsync(](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx)請注意複數""),在單個事務中獲取多條消息。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-143">Instead, you can call [CloudQueue.GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (note the plural 's'), which gets multiple messages in a single transaction.</span></span> <span data-ttu-id="8e9ef-144">Azure 儲存佇列的事務成本非常低,因此在大多數情況下,對成本的影響並不大。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-144">The transaction costs for Azure Storage Queues are very low, so the impact on costs is not substantial in most scenarios.</span></span>
- <span data-ttu-id="8e9ef-145">佇列消息處理代碼中的緊密迴圈會導致 CPU 關聯性,而 CPU 關聯性不會有效地利用多核 VM。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-145">The tight loop in the queue message-processing code causes CPU affinity, which does not utilize multi-core VMs efficiently.</span></span> <span data-ttu-id="8e9ef-146">更好的設計將使用任務並行性並行運行多個非同步任務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-146">A better design would use task parallelism to run several async tasks in parallel.</span></span>
- <span data-ttu-id="8e9ef-147">佇列消息處理只有基本的異常處理。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-147">Queue message-processing has only rudimentary exception handling.</span></span> <span data-ttu-id="8e9ef-148">例如,程式碼不處理[有害訊息](https://msdn.microsoft.com/library/ms789028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-148">For example, the code doesn't handle [poison messages](https://msdn.microsoft.com/library/ms789028.aspx).</span></span> <span data-ttu-id="8e9ef-149">(當消息處理導致異常時,您必須記錄錯誤並刪除消息,否則輔助角色將再次嘗試處理該錯誤,並且迴圈將無限期地繼續。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-149">(When message processing causes an exception, you have to log the error and delete the message, or the worker role will try to process it again, and the loop will continue indefinitely.)</span></span>

### <a name="sql-queries-are-unbounded"></a><span data-ttu-id="8e9ef-150">SQL 查詢未繫結</span><span class="sxs-lookup"><span data-stu-id="8e9ef-150">SQL queries are unbounded</span></span>

<span data-ttu-id="8e9ef-151">當前修復代碼對索引頁的查詢可能返回的行數沒有限制。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-151">Current Fix It code places no limit on how many rows the queries for Index pages might return.</span></span> <span data-ttu-id="8e9ef-152">如果資料庫中輸入了大量任務,則接收的結果清單的大小可能會導致性能問題。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-152">If a large volume of tasks is entered into the database, the size of the resulting lists received could cause performance issues.</span></span> <span data-ttu-id="8e9ef-153">解決方案是實現分頁。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-153">The solution is to implement paging.</span></span> <span data-ttu-id="8e9ef-154">例如,請參閱在[ASP.NET mVC 應用程式中使用實體框架對實體框架進行排序、篩選和分頁](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-154">For an example, see [Sorting, Filtering, and Paging with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span>

### <a name="view-models-recommended"></a><span data-ttu-id="8e9ef-155">檢視推薦的模型</span><span class="sxs-lookup"><span data-stu-id="8e9ef-155">View models recommended</span></span>

<span data-ttu-id="8e9ef-156">修復它應用使用 FixItTask 實體類在控制器和檢視之間傳遞資訊。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-156">The Fix It app uses the FixItTask entity class to pass information between the controller and the view.</span></span> <span data-ttu-id="8e9ef-157">最佳做法是使用視圖模型。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-157">A best practice is to use view models.</span></span> <span data-ttu-id="8e9ef-158">域模型(例如 FixItTask 實體類)是圍繞數據持久性所需的內容設計的,而視圖模型可以設計為數據表示。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-158">The domain model (e.g., the FixItTask entity class) is designed around what is needed for data persistence, while a view model can be designed for data presentation.</span></span> <span data-ttu-id="8e9ef-159">有關詳細資訊,請參閱[12 ASP.NET MVC 最佳實務](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-159">For more information, see [12 ASP.NET MVC Best Practices](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).</span></span>

### <a name="secure-image-blob-recommended"></a><span data-ttu-id="8e9ef-160">建議使用安全映像 blob</span><span class="sxs-lookup"><span data-stu-id="8e9ef-160">Secure image blob recommended</span></span>

<span data-ttu-id="8e9ef-161">Fix It 應用將上傳的圖像存儲為公共圖像,這意味著找到 URL 的任何人都可以訪問這些圖像。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-161">The Fix It app stores uploaded images as public, meaning that anyone who finds the URL can access the images.</span></span> <span data-ttu-id="8e9ef-162">圖像可以保護而不是公開。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-162">The images could be secured instead of public.</span></span>

### <a name="no-powershell-automation-scripts-for-queues"></a><span data-ttu-id="8e9ef-163">沒有在佇列的 PowerShell 自動化文稿</span><span class="sxs-lookup"><span data-stu-id="8e9ef-163">No PowerShell automation scripts for queues</span></span>

<span data-ttu-id="8e9ef-164">示例 PowerShell 自動化文本僅針對完全在 Azure 應用服務 Web 應用中運行的修復它的基本版本編寫。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-164">Sample PowerShell automation scripts were written only for the base version of Fix It that runs entirely in Azure App Service Web Apps.</span></span> <span data-ttu-id="8e9ef-165">我們沒有提供用於設置和部署到 Web 應用以及佇列處理所需的雲端服務環境的腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-165">We haven't provided scripts for setting up and deploying to the web app plus Cloud Service environment required for queue processing.</span></span>

### <a name="special-handling-for-html-codes-in-user-input"></a><span data-ttu-id="8e9ef-166">使用者輸入 HTML 代碼的特殊處理</span><span class="sxs-lookup"><span data-stu-id="8e9ef-166">Special handling for HTML codes in user input</span></span>

<span data-ttu-id="8e9ef-167">ASP.NET通過在使用者輸入文本框中輸入腳本,自動防止惡意用戶嘗試跨網站腳本攻擊的多種方式。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-167">ASP.NET automatically prevents many ways in which malicious users might attempt cross-site scripting attacks by entering script in user input text boxes.</span></span> <span data-ttu-id="8e9ef-168">MVC`DisplayFor`幫助程式用於顯示任務標題和註釋,自動對其進行 HTML 編碼它發送到瀏覽器的值。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-168">And the MVC `DisplayFor` helper used to display task titles and notes automatically HTML-encodes values that it sends to the browser.</span></span> <span data-ttu-id="8e9ef-169">但在生產應用中,您可能需要採取其他措施。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-169">But in a production app you might want to take additional measures.</span></span> <span data-ttu-id="8e9ef-170">有關詳細資訊,請參閱ASP.NET[中的要求驗證](https://msdn.microsoft.com/library/hh882339.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-170">For more information, see [Request Validation in ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).</span></span>

<a id="bestpractices"></a>
## <a name="best-practices"></a><span data-ttu-id="8e9ef-171">最佳作法</span><span class="sxs-lookup"><span data-stu-id="8e9ef-171">Best practices</span></span>

<span data-ttu-id="8e9ef-172">以下是在修復 It 應用的原始版本的代碼審查和測試中發現后修復的一些問題。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-172">Following are some issues that were fixed after being discovered in code review and testing of the original version of the Fix It app.</span></span> <span data-ttu-id="8e9ef-173">有些是由於原始編碼器不知道特定的最佳實踐造成的,有些只是因為代碼編寫得很快,並非針對發佈的軟體。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-173">Some were caused by the original coder not being aware of a particular best practice, some simply because the code was written quickly and wasn't intended for released software.</span></span> <span data-ttu-id="8e9ef-174">我們在這裡列出問題,以防我們從這次審查和測試中學到的東西對正在開發 Web 應用程式的其他人有説明。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-174">We're listing the issues here in case there's something we learned from this review and testing that might be helpful to others who are also developing web apps.</span></span>

### <a name="dispose-the-database-repository"></a><span data-ttu-id="8e9ef-175">處置資料庫儲存庫</span><span class="sxs-lookup"><span data-stu-id="8e9ef-175">Dispose the database repository</span></span>

<span data-ttu-id="8e9ef-176">類`FixItTaskRepository`必須釋放實體框架`DbContext`實例。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-176">The `FixItTaskRepository` class must dispose the Entity Framework `DbContext` instance.</span></span> <span data-ttu-id="8e9ef-177">我們通過在`FixItTaskRepository`類中`IDisposable`實現 來實現此情況:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-177">We did this by implementing `IDisposable` in the `FixItTaskRepository` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

<span data-ttu-id="8e9ef-178">請注意,AutoFac 將自動`FixItTaskRepository`釋放 實例,因此我們不需要顯式處置它。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-178">Note that AutoFac will automatically dispose the `FixItTaskRepository` instance, so we don't need to explicitly dispose it.</span></span>

<span data-ttu-id="8e9ef-179">另一個選項是從 中`DbContext`刪除成員變數`FixItTaskRepository`,而是在語句內在`DbContext`每個 儲存庫方法中創建`using`一個局部變數。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-179">Another option is to remove the `DbContext` member variable from `FixItTaskRepository`, and instead create a local `DbContext` variable within each repository method, inside a `using` statement.</span></span> <span data-ttu-id="8e9ef-180">例如：</span><span class="sxs-lookup"><span data-stu-id="8e9ef-180">For example:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a><span data-ttu-id="8e9ef-181">使用 DI 註冊單例</span><span class="sxs-lookup"><span data-stu-id="8e9ef-181">Register singletons as such with DI</span></span>

<span data-ttu-id="8e9ef-182">由於只需要`PhotoService`類`Logger`和 類的一個實例,因此這些類應註冊為*DependenciesConfig.cs*[中依賴項注入的單個實例](https://code.google.com/p/autofac/wiki/InstanceScope):</span><span class="sxs-lookup"><span data-stu-id="8e9ef-182">Since only one instance of the `PhotoService` class and `Logger` class is needed, these classes should be [registered as single instances for dependency injection](https://code.google.com/p/autofac/wiki/InstanceScope) in *DependenciesConfig.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a><span data-ttu-id="8e9ef-183">安全性:不向使用者顯示錯誤詳細資訊</span><span class="sxs-lookup"><span data-stu-id="8e9ef-183">Security: Don't show error details to users</span></span>

<span data-ttu-id="8e9ef-184">原始修復 It 應用沒有通用錯誤頁,只是讓所有異常都冒泡到 UI 上,因此某些異常(如資料庫連接錯誤)可能會導致向瀏覽器顯示完整的堆疊跟蹤。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-184">The original Fix It app didn't have a generic error page and just let all exceptions bubble up to the UI, so some exceptions such as database connection errors could result in a full stack trace being displayed to the browser.</span></span> <span data-ttu-id="8e9ef-185">詳細的錯誤信息有時可能促進惡意用戶的攻擊。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-185">Detailed error information can sometimes facilitate attacks by malicious users.</span></span> <span data-ttu-id="8e9ef-186">解決方案是記錄異常詳細資訊,並將錯誤頁顯示給不包含錯誤詳細資訊的使用者。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-186">The solution is to log the exception details and display an error page to the user that doesn't include error details.</span></span> <span data-ttu-id="8e9ef-187">修復它應用已經記錄,為了顯示錯誤頁面,我們添加了`<customErrors mode=On>`Web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-187">The Fix It app was already logging, and in order to display an error page, we added `<customErrors mode=On>` in the Web.config file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

<span data-ttu-id="8e9ef-188">默認情況下,這將導致*顯示檢視\共用\Error.cshtml*以查找錯誤。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-188">By default this causes *Views\Shared\Error.cshtml* to be displayed for errors.</span></span> <span data-ttu-id="8e9ef-189">您可以自訂*Error.cshtml*或創建自己的錯誤頁面檢視並`defaultRedirect`添加 屬性。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-189">You can customize *Error.cshtml* or create your own error page view and add a `defaultRedirect` attribute.</span></span> <span data-ttu-id="8e9ef-190">您還可以為特定錯誤指定不同的錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-190">You can also specify different error pages for specific errors.</span></span>

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a><span data-ttu-id="8e9ef-191">安全性:僅允許其建立者編輯工作</span><span class="sxs-lookup"><span data-stu-id="8e9ef-191">Security: only allow a task to be edited by its creator</span></span>

<span data-ttu-id="8e9ef-192">"儀錶板索引"頁僅顯示登錄使用者創建的任務,但惡意使用者可以創建具有其他使用者任務的 ID 的 URL。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-192">The Dashboard Index page only shows tasks created by the logged-on user, but a malicious user could create a URL with an ID to another user's task.</span></span> <span data-ttu-id="8e9ef-193">我們*DashboardController.cs 中*添加了代碼,以在這種情況下返回 404:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-193">We added code in *DashboardController.cs* to return a 404 in that case:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a><span data-ttu-id="8e9ef-194">不要吞咽異常</span><span class="sxs-lookup"><span data-stu-id="8e9ef-194">Don't swallow exceptions</span></span>

<span data-ttu-id="8e9ef-195">原始修復 It 應用程式在紀錄 SQL 查詢產生的例外後剛剛傳回 null:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-195">The original Fix It app just returned null after logging an exception that resulted from a SQL query:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

<span data-ttu-id="8e9ef-196">這將使用戶看起來好像查詢成功,但只是沒有返回任何行。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-196">This would make it look to the user as if the query succeeded but just didn't return any rows.</span></span> <span data-ttu-id="8e9ef-197">解決方案是在捕獲和日誌記錄後重新引發異常:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-197">Solution is to re-throw the exception after catching and logging:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a><span data-ttu-id="8e9ef-198">擷取輔助角色中的所有例外</span><span class="sxs-lookup"><span data-stu-id="8e9ef-198">Catch all exceptions in worker roles</span></span>

<span data-ttu-id="8e9ef-199">輔助角色中的任何未處理異常都將導致 VM 被回收,因此您希望在 try-catch 塊中包裝所有操作,並處理所有異常。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-199">Any unhandled exceptions in a worker role will cause the VM to be recycled, so you want to wrap everything you do in a try-catch block and handle all exceptions.</span></span>

### <a name="specify-length-for-string-properties-in-entity-classes"></a><span data-ttu-id="8e9ef-200">指定實體類別的字串屬性的長度</span><span class="sxs-lookup"><span data-stu-id="8e9ef-200">Specify length for string properties in entity classes</span></span>

<span data-ttu-id="8e9ef-201">為了顯示簡單代碼,修復它應用的原始版本沒有指定 FixItTask 實體欄位的長度,因此在資料庫中將其定義為 varchar(max)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-201">In order to display simple code, the original version of the Fix It app didn't specify lengths for the fields of the FixItTask entity, and as a result they were defined as varchar(max) in the database.</span></span> <span data-ttu-id="8e9ef-202">因此,UI 將接受幾乎任何數量的輸入。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-202">As a result, the UI would accept almost any amount of input.</span></span> <span data-ttu-id="8e9ef-203">指定長度設定適用於網頁中的使用者輸入和資料庫中的欄大小的限制:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-203">Specifying lengths sets limits that apply both to user input in the web page and column size in the database:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a><span data-ttu-id="8e9ef-204">當私人成員不需要更改時,將它們標記為唯讀</span><span class="sxs-lookup"><span data-stu-id="8e9ef-204">Mark private members as readonly when they aren't expected to change</span></span>

<span data-ttu-id="8e9ef-205">例如,在類中`DashboardController`,將`FixItTaskRepository`建立一個實例,並且不需要更改,所以我們將其定義為[唯讀](https://msdn.microsoft.com/library/acdd6hb7.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-205">For example, in the `DashboardController` class an instance of `FixItTaskRepository` is created and isn't expected to change, so we defined it as [readonly](https://msdn.microsoft.com/library/acdd6hb7.aspx).</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a><span data-ttu-id="8e9ef-206">使用清單。任何()而不是清單。計數() &gt; 0</span><span class="sxs-lookup"><span data-stu-id="8e9ef-206">Use list.Any() instead of list.Count() &gt; 0</span></span>

<span data-ttu-id="8e9ef-207">如果您所關心的只是清單中的一個或多個項是否符合指定的條件,請使用[Any](https://msdn.microsoft.com/library/bb534972.aspx)方法,因為它在找到符合條件的項後立即返回`Count`,而 該方法始終必須遍遍遍每個項。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-207">If you all you care about is whether one or more items in a list fit the specified criteria, use the [Any](https://msdn.microsoft.com/library/bb534972.aspx) method, because it returns as soon as an item fitting the criteria is found, whereas the `Count` method always has to iterate through every item.</span></span> <span data-ttu-id="8e9ef-208">儀表板*索引.cshtml*檔案最初具有以下代碼:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-208">The Dashboard *Index.cshtml* file originally had this code:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

<span data-ttu-id="8e9ef-209">我們將其更改為:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-209">We changed it to this:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a><span data-ttu-id="8e9ef-210">使用 MVC 說明器在 MVC 檢視中產生網址</span><span class="sxs-lookup"><span data-stu-id="8e9ef-210">Generate URLs in MVC views using MVC helpers</span></span>

<span data-ttu-id="8e9ef-211">對於主頁上的「**修復 It」** 按鈕,「修復它」應用硬編碼錨點元素:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-211">For the **Create a Fix It** button on the home page, the Fix It app hard coded an anchor element:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

<span data-ttu-id="8e9ef-212">對於像這樣的檢視/操作連結,最好使用[網址.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML 幫助程式,例如:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-212">For View/Action links like this it's better to use the [Url.Action](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) HTML helper, for example:</span></span>

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a><span data-ttu-id="8e9ef-213">使用任務.延遲而不是線程.睡眠在輔助角色中</span><span class="sxs-lookup"><span data-stu-id="8e9ef-213">Use Task.Delay instead of Thread.Sleep in worker role</span></span>

<span data-ttu-id="8e9ef-214">新專案範本將工作角色的範例`Thread.Sleep`代碼放入其中,但導致線程處於睡眠狀態可能會導致線程池生成其他不必要的線程。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-214">The new-project template puts `Thread.Sleep` in the sample code for a worker role, but causing the thread to sleep can cause the thread pool to spawn additional unnecessary threads.</span></span> <span data-ttu-id="8e9ef-215">您可以使用[Task.delay](https://msdn.microsoft.com/library/hh139096.aspx)來避免這種情況。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-215">You can avoid that by using [Task.Delay](https://msdn.microsoft.com/library/hh139096.aspx) instead.</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a><span data-ttu-id="8e9ef-216">避免非空隙</span><span class="sxs-lookup"><span data-stu-id="8e9ef-216">Avoid async void</span></span>

<span data-ttu-id="8e9ef-217">如果非同步方法不需要傳回值,則傳`Task`回`void`類型 而不是 。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-217">If an async method doesn't need to return a value, return a `Task` type rather than `void`.</span></span>

<span data-ttu-id="8e9ef-218">這個範例來自類別`FixItQueueManager`:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-218">This example is from the `FixItQueueManager` class:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

<span data-ttu-id="8e9ef-219">應僅對`async void`頂級事件處理程式使用。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-219">You should use `async void` only for top-level event handlers.</span></span> <span data-ttu-id="8e9ef-220">如果將方法定義為`async void`,調用方無法**等待**該方法或捕獲方法引發的任何異常。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-220">If you define a method as `async void`, the caller cannot **await** the method or catch any exceptions the method throws.</span></span> <span data-ttu-id="8e9ef-221">有關詳細資訊,請參閱[非同步編程中的最佳做法](https://msdn.microsoft.com/magazine/jj991977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-221">For more information, see [Best Practices in Asynchronous Programming](https://msdn.microsoft.com/magazine/jj991977.aspx).</span></span>

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a><span data-ttu-id="8e9ef-222">使用取消權杖從輔助角色循環中斷</span><span class="sxs-lookup"><span data-stu-id="8e9ef-222">Use a cancellation token to break from worker role loop</span></span>

<span data-ttu-id="8e9ef-223">通常,輔助角色上的**Run**方法包含無限迴圈。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-223">Typically, the **Run** method on a worker role contains an infinite loop.</span></span> <span data-ttu-id="8e9ef-224">當輔助角色停止時,將調用[角色入口點.onStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-224">When the worker role is stopping, the [RoleEntryPoint.OnStop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) method is called.</span></span> <span data-ttu-id="8e9ef-225">應使用此方法取消在**Run**方法內完成的工作並正常退出。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-225">You should use this method to cancel the work that is being done inside the **Run** method and exit gracefully.</span></span> <span data-ttu-id="8e9ef-226">否則,進程可能在操作過程中終止。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-226">Otherwise, the process might be terminated in the middle of an operation.</span></span>

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a><span data-ttu-id="8e9ef-227">選擇宣告自動 MIME 嗅探程序</span><span class="sxs-lookup"><span data-stu-id="8e9ef-227">Opt out of Automatic MIME Sniffing Procedure</span></span>

<span data-ttu-id="8e9ef-228">在某些情況下,Internet Explorer 報告 MIME 類型與 Web 伺服器指定的類型不同。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-228">In some cases, Internet Explorer reports a MIME type different than the type specified by the web server.</span></span> <span data-ttu-id="8e9ef-229">例如,如果 Internet Explorer 在使用 HTTP 回應標頭內容類型:文本/純文交付的檔中尋找 HTML 內容,則 Internet Explorer 確定內容應呈現為 HTML。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-229">For instance, if Internet Explorer finds HTML content in a file delivered with the HTTP response header Content-Type: text/plain, Internet Explorer determines that the content should be rendered as HTML.</span></span> <span data-ttu-id="8e9ef-230">遺憾的是,這種"MIME嗅探"還可能導致託管不受信任的內容的伺服器出現安全問題。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-230">Unfortunately, this "MIME-sniffing" can also lead to security problems for servers hosting untrusted content.</span></span> <span data-ttu-id="8e9ef-231">為了解決這個問題,Internet Explorer 8 對 MIME 類型的確定代碼進行了一些更改,並允許應用程式開發人員[選擇宣告 MIME 嗅探](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-231">To combat this problem, Internet Explorer 8 has made a number of changes to MIME-type determination code and allows application developers to [opt out of MIME-sniffing](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx).</span></span> <span data-ttu-id="8e9ef-232">以下代碼已新增到*Web.config 檔案中*。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-232">The following code was added to the *Web.config* file.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a><span data-ttu-id="8e9ef-233">實現捆綁和最小化</span><span class="sxs-lookup"><span data-stu-id="8e9ef-233">Enable bundling and minification</span></span>

<span data-ttu-id="8e9ef-234">當 Visual Studio 創建新的 Web 專案時,預設情況下不會啟用 JavaScript 檔的捆綁和小化。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-234">When Visual Studio creates a new web project, bundling and minification of JavaScript files is not enabled by default.</span></span> <span data-ttu-id="8e9ef-235">我們在BundleConfig.cs中添加了一行代碼:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-235">We added a line of code in BundleConfig.cs:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a><span data-ttu-id="8e9ef-236">為身份驗證 Cookie 設定過期逾時</span><span class="sxs-lookup"><span data-stu-id="8e9ef-236">Set an expiration time-out for authentication cookies</span></span>

<span data-ttu-id="8e9ef-237">默認情況下,身份驗證 Cookie 將在兩周後過期。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-237">By default, authentication cookies expire in two weeks.</span></span> <span data-ttu-id="8e9ef-238">更短的時間更安全。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-238">A shorter time is more secure.</span></span> <span data-ttu-id="8e9ef-239">您可以在*StartupAuth.cs*中變更這個設定:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-239">You can change this setting in *StartupAuth.cs*:</span></span>

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a><span data-ttu-id="8e9ef-240">如何從本地電腦上的 Visual Studio 執行應用</span><span class="sxs-lookup"><span data-stu-id="8e9ef-240">How to run the app from Visual Studio on your local computer</span></span>

<span data-ttu-id="8e9ef-241">有兩種方法可以運行修復它應用:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-241">There are two ways to run the Fix It app:</span></span>

- <span data-ttu-id="8e9ef-242">運行將新任務直接寫入 SQL 資料庫的基本應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-242">Run the base application that writes new tasks directly to the SQL database.</span></span>
- <span data-ttu-id="8e9ef-243">使用佇列和後端服務運行應用程式以建立任務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-243">Run the application using a queue plus a backend service to create tasks.</span></span> <span data-ttu-id="8e9ef-244">佇列模式在以[隊列為中心的工作模式](queue-centric-work-pattern.md)一章中描述。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-244">The queue pattern is described in the chapter [Queue-Centric Work Pattern](queue-centric-work-pattern.md).</span></span>

<a id="runbase"></a>
### <a name="run-the-base-application"></a><span data-ttu-id="8e9ef-245">執行基本應用程式</span><span class="sxs-lookup"><span data-stu-id="8e9ef-245">Run the base application</span></span>

1. <span data-ttu-id="8e9ef-246">安裝[視覺工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="8e9ef-246">Install [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>
2. <span data-ttu-id="8e9ef-247">為[.NET 安裝用於視覺工作室的 Azure SDK。](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8e9ef-247">Install the [Azure SDK for .NET for Visual Studio](https://azure.microsoft.com/downloads/).</span></span>
3. <span data-ttu-id="8e9ef-248">從[MSDN 程式庫](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)下載 .zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-248">Download the .zip file from the [MSDN Code Gallery](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).</span></span>
4. <span data-ttu-id="8e9ef-249">在「檔案資源管理器」中,右鍵按下 .zip 檔案並按下「屬性」,然後在「屬性」視窗中按下「取消阻止」。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-249">In File Explorer, right-click the .zip file and click Properties, then in the Properties window click Unblock.</span></span>
5. <span data-ttu-id="8e9ef-250">解壓縮檔。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-250">Unzip the file.</span></span>
6. <span data-ttu-id="8e9ef-251">按兩下 .sln 檔以啟動可視化工作室。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-251">Double-click the .sln file to launch Visual Studio.</span></span>
7. <span data-ttu-id="8e9ef-252">在 **'工具'** 選單中,按下**NuGet 套件管理員**,然後單擊**套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-252">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>
8. <span data-ttu-id="8e9ef-253">在包管理器主控台 (PMC) 中,按一下「還原」。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-253">In the Package Manager Console (PMC), click Restore.</span></span>
9. <span data-ttu-id="8e9ef-254">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-254">Exit Visual Studio.</span></span>
10. <span data-ttu-id="8e9ef-255">啟動[Azure 儲存模擬器](/azure/storage/common/storage-use-emulator)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-255">Start the [Azure storage emulator](/azure/storage/common/storage-use-emulator).</span></span>
11. <span data-ttu-id="8e9ef-256">重新啟動 Visual Studio,打開在上一步中關閉的解決方案檔。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-256">Restart Visual Studio, opening the solution file you closed in the previous step.</span></span>
12. <span data-ttu-id="8e9ef-257">確保 FixIt 專案設置為啟動項目,然後按 CTRL_F5 運行該專案。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-257">Make sure the FixIt project is set as the startup project, and then press CTRL+F5 to run the project.</span></span>

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a><span data-ttu-id="8e9ef-258">使用佇列處理執行應用程式</span><span class="sxs-lookup"><span data-stu-id="8e9ef-258">Run the application with queue processing</span></span>

1. <span data-ttu-id="8e9ef-259">按照[運行基本應用程式](#runbase)的說明操作,然後關閉瀏覽器並關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-259">Follow the directions for [Run the base application](#runbase), and then close the browser and close Visual Studio.</span></span>
2. <span data-ttu-id="8e9ef-260">使用管理員許可權啟動可視化工作室。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-260">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="8e9ef-261">(您將使用 Azure 計算模擬器,這需要管理員許可權。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-261">(You'll be using the Azure compute emulator, and that requires administrator privileges.)</span></span>
3. <span data-ttu-id="8e9ef-262">在*MyFixIt*專案中的應用程式*Web.config*檔案中(Web 專案`appSettings/UseQueues`),將的值 更改為「true」:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-262">In the application *Web.config* file in the *MyFixIt* project (the web project), change the value of `appSettings/UseQueues` to "true":</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. <span data-ttu-id="8e9ef-263">如果[Azure 儲存模擬器](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx)未運行,則重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-263">If the [Azure storage emulator](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) isn't still running, start it again.</span></span>
5. <span data-ttu-id="8e9ef-264">同時運行修復 It Web 專案和 MyFixIt 雲端服務專案。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-264">Run the FixIt web project and the MyFixItCloudService project simultaneously.</span></span>

    <span data-ttu-id="8e9ef-265">使用視覺工作室:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-265">Using Visual Studio:</span></span>

   1. <span data-ttu-id="8e9ef-266">按**F5**以運行 FixIt 專案。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-266">Press **F5** to run the FixIt project.</span></span>
   2. <span data-ttu-id="8e9ef-267">在**解決方案資源管理器**中,右鍵單擊 MyFixIt雲端服務專案,然後單擊 **「調試** > **啟動新實例**」。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-267">In **Solution Explorer**, right-click the MyFixItCloudService project, and then click **Debug** > **Start New Instance**.</span></span>

    <span data-ttu-id="8e9ef-268">使用視覺化工作室 2013 快速網頁:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-268">Using Visual Studio 2013 Express for Web:</span></span>

   3. <span data-ttu-id="8e9ef-269">在解決方案資源管理員中,右鍵按下 FixIt 解決方案並選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-269">In Solution Explorer, right-click the FixIt solution and select **Properties**.</span></span>
   4. <span data-ttu-id="8e9ef-270">選擇**多個啟動項目**。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-270">Select **Multiple Startup Projects**.</span></span>
   5. <span data-ttu-id="8e9ef-271">在 MyFixIt 和 MyFixIt雲端服務下的 **「操作**」下拉清單中,選擇 **「開始**」。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-271">In the **Action** dropdown list under MyFixIt and MyFixItCloudService, select **Start**.</span></span>
   6. <span data-ttu-id="8e9ef-272">按一下 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-272">Click **OK**.</span></span>
   7. <span data-ttu-id="8e9ef-273">按 **F5** 執行這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-273">Press **F5** to run both projects.</span></span>

      <span data-ttu-id="8e9ef-274">運行 MyFixItCloud 服務專案時,Visual Studio 將啟動 Azure 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-274">When you run the MyFixItCloudService project, Visual Studio starts the Azure compute emulator.</span></span> <span data-ttu-id="8e9ef-275">根據您的防火牆配置,您可能需要允許模擬器通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-275">Depending on your firewall configuration, you might need to allow the emulator through the firewall.</span></span>

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a><span data-ttu-id="8e9ef-276">如何使用 Windows PowerShell 文稿將基本應用部署到 Azure 應用服務 Web 應用</span><span class="sxs-lookup"><span data-stu-id="8e9ef-276">How to deploy the base app to Azure App Service Web Apps by using the Windows PowerShell scripts</span></span>

<span data-ttu-id="8e9ef-277">為了說明[「自動執行所有內容」](automate-everything.md)模式,修復 It 應用附帶了在 Azure 中設置環境並將專案部署到新環境的腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-277">To illustrate the [Automate Everything](automate-everything.md) pattern, the Fix It app is supplied with scripts that set up an environment in Azure and deploy the project to the new environment.</span></span> <span data-ttu-id="8e9ef-278">以下說明說明如何使用腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-278">The following instructions explain how to use the scripts.</span></span>

<span data-ttu-id="8e9ef-279">如果要在 Azure 中運行而不使用佇列,並且所做的更改是為了在本地使用佇列運行,請確保在繼續執行以下說明之前將 Use 佇列應用設置值設定為 false。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-279">If you want to run in Azure without using queues, and you made the changes to run locally with queues, make sure you set the UseQueues appSetting value back to false before proceeding with the following instructions.</span></span>

<span data-ttu-id="8e9ef-280">這些說明假定您已在本地下載並運行修復 It 解決方案,並且您具有 Azure 帳戶或已授權管理的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-280">These instructions assume you have already downloaded and run the Fix It solution locally, and that you have an Azure account or have an Azure subscription that you are authorized to manage.</span></span>

1. <span data-ttu-id="8e9ef-281">安裝**Azure PowerShell**主控台。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-281">Install the **Azure PowerShell** console.</span></span> <span data-ttu-id="8e9ef-282">如需指示，請參閱 [如何安裝和設定 Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-282">For instructions, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).</span></span>

    <span data-ttu-id="8e9ef-283">此自定義主控台配置為與 Azure 訂閱配合使用。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-283">This customized console is configured to work with your Azure subscription.</span></span> <span data-ttu-id="8e9ef-284">Azure 模組安裝在 *「程式檔」* 目錄中,並在每次使用 Azure PowerShell 控制台時自動匯入。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-284">The Azure module is installed in the *Program Files* directory and is automatically imported on every use of the Azure PowerShell console.</span></span>

    <span data-ttu-id="8e9ef-285">如果喜歡在不同的主機程式(如 Windows PowerShell ISE)中工作,請確保使用[導入模組](https://go.microsoft.com/fwlink/?LinkID=141553)cmdlet 導入 Azure 模組或使用 Azure 模組中的命令觸發模組的自動導入。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-285">If you prefer to work in a different host program, such as Windows PowerShell ISE, be sure to use the [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) cmdlet to import the Azure module or use a command in the Azure module to trigger automatic importing of the module.</span></span>
2. <span data-ttu-id="8e9ef-286">使用 **「以管理員身份執行」** 選項啟動 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-286">Start Azure PowerShell with the **Run as administrator** option.</span></span>
3. <span data-ttu-id="8e9ef-287">執行[設定執行原則](https://go.microsoft.com/fwlink/p/?linkid=293941)「cmdlet 以將 Azure`RemoteSigned`PowerShell 執行政策設定為 。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-287">Run the [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) cmdlet to set the Azure PowerShell execution policy to `RemoteSigned`.</span></span> <span data-ttu-id="8e9ef-288">輸入**Y(** 對於是)以完成策略更改。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-288">Enter **Y** (for Yes) to complete the policy change.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    <span data-ttu-id="8e9ef-289">這個設定讓您能夠執行未進行數位簽名的本地文稿。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-289">This setting enables you to run local scripts that aren't digitally signed.</span></span> <span data-ttu-id="8e9ef-290">(您還可以將執行策略設置為`Unrestricted`,這將在以後無需取消阻止步驟,但出於安全原因不建議這樣做。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-290">(You can also set the execution policy to `Unrestricted`, which would eliminate the need for the unblock step later, but this is not recommended for security reasons.)</span></span>
4. <span data-ttu-id="8e9ef-291">運行`Add-AzureAccount`cmdlet 以使用您的帳戶認證設定 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-291">Run the `Add-AzureAccount` cmdlet to set up PowerShell with credentials for your account.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    <span data-ttu-id="8e9ef-292">這些憑據將在一段時間後過期,您必須重新運行`Add-AzureAccount`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-292">These credentials expire after a period of time and you have to re-run the `Add-AzureAccount` cmdlet.</span></span> <span data-ttu-id="8e9ef-293">在編寫此電子書時,憑據過期前的時間限制為 12 小時。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-293">As this e-book is being written, the time limit before credentials expire is 12 hours.</span></span>
5. <span data-ttu-id="8e9ef-294">如果您有多個訂閱,請使用選擇 Azure 訂閱 cmdlet 指定要在 中創建測試環境的訂閱。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-294">If you have multiple subscriptions, use the Select-AzureSubscription cmdlet to specify the subscription you want to create the test environment in.</span></span>
6. <span data-ttu-id="8e9ef-295">使用`Get-AzurePublishSettingsFile`和`Import-AzurePublishSettingsFile`cmdlet 匯入同一 Azure 訂閱的管理證書。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-295">Import a management certificate for the same Azure subscription by using the `Get-AzurePublishSettingsFile` and `Import-AzurePublishSettingsFile` cmdlets.</span></span> <span data-ttu-id="8e9ef-296">第一個 cmdlet 下載憑證檔,在第二個 cmdlet 中,您可以指定該檔案的位置以匯入它。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-296">The first of these cmdlets downloads a certificate file, and in the second one you specify the location of that file in order to import it.</span></span> > [!IMPORTANT]
   > <span data-ttu-id="8e9ef-297">將下載的檔案保存在安全位置,或完成後將其刪除,因為它包含可用於管理 Azure 服務的證書。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-297">Keep the downloaded file in a safe location or delete it when you're done with it, because it contains a certificate that can be used to manage your Azure services.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    <span data-ttu-id="8e9ef-298">該證書用於 REST API 呼叫,該呼叫檢測開發機的 IP 位址,以便在 SQL 資料庫伺服器上設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-298">The certificate is used for a REST API call that detects the development machine's IP address in order to set a firewall rule on the SQL Database server.</span></span>
7. <span data-ttu-id="8e9ef-299">執行[「設定位置](https://go.microsoft.com/fwlink/p/?linkid=293912)cmdlet」(`cd``chdir``sl`別名為 和 ),以瀏覽到包含文稿的目錄。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-299">Run the [Set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) cmdlet (aliases are `cd`, `chdir`, and `sl`) to navigate to the directory that contains the scripts.</span></span> <span data-ttu-id="8e9ef-300">(它們位於"修復它"解決方案資料夾中的*自動化*資料夾中。如果任何目錄名稱包含空格,則將路徑放入引號中。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-300">(They're located in the *Automation* folder in the Fix It solution folder.) Put the path in quotes if any of the directory names contain spaces.</span></span> <span data-ttu-id="8e9ef-301">例如,要導航到目錄,`c:\Sample Apps\FixIt\Automation`可以輸入以下命令:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-301">For example, to navigate to the `c:\Sample Apps\FixIt\Automation` directory you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. <span data-ttu-id="8e9ef-302">要允許 Windows PowerShell 運行這些文稿,請使用[取消阻止檔案](https://go.microsoft.com/fwlink/p/?linkid=294021)cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-302">To allow Windows PowerShell to run these scripts, use the [Unblock-File](https://go.microsoft.com/fwlink/p/?linkid=294021) cmdlet.</span></span> <span data-ttu-id="8e9ef-303">(腳本被阻止,因為它們是從 Internet 下載的。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-303">(The scripts are blocked because they were downloaded from the Internet.)</span></span>

    > [!WARNING]
    > <span data-ttu-id="8e9ef-304">安全性`Unblock-File`- 在運行任何文稿或可執行檔之前,在記事本中打開該檔,檢查命令,並驗證它們不包含任何惡意代碼。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-304">Security - Before running `Unblock-File` on any script or executable file, open the file in Notepad, examine the commands, and verify that they do not contain any malicious code.</span></span>

    <span data-ttu-id="8e9ef-305">例如,以下命令在當前目錄中的所有文稿`Unblock-File`上運行 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-305">For example, the following command runs the `Unblock-File` cmdlet on all scripts in the current directory.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. <span data-ttu-id="8e9ef-306">要為基礎創建 Web 應用(無佇列處理)修復它應用,請執行環境創建腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-306">To create the web app for the base (no queues processing) Fix It app, run the environment creation script.</span></span>

    <span data-ttu-id="8e9ef-307">所需的`Name`參數指定資料庫的名稱,並且也用於腳本創建的存儲帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-307">The required `Name` parameter specifies the name of the database and is also used for the storage account that the script creates.</span></span> <span data-ttu-id="8e9ef-308">名稱在azurewebsites.net域中必須全域唯一。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-308">The name must be globally unique within the azurewebsites.net domain.</span></span> <span data-ttu-id="8e9ef-309">如果指定的名稱不唯一(如 Fixit 或 Test(甚至如示例中的 fixitdemo),`New-AzureWebsite`則 cmdlet 失敗,並出現報告衝突的內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-309">If you specify a name that is not unique, like Fixit or Test (or even as in the example, fixitdemo), the `New-AzureWebsite` cmdlet fails with an Internal Error that reports a conflict.</span></span> <span data-ttu-id="8e9ef-310">該文本將名稱轉換為所有小寫,以符合 Web 應用、存儲帳戶和資料庫的名稱要求。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-310">The script converts the name to all lower-case to comply with name requirements for web apps, storage accounts, and databases.</span></span>

    <span data-ttu-id="8e9ef-311">所需`SqlDatabasePassword`參數指定將為 SQL 資料庫創建的管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-311">The required `SqlDatabasePassword` parameter specifies the password for the admin account that will be created for SQL Database.</span></span> <span data-ttu-id="8e9ef-312">不要在密碼中包含特殊的 XML 字元(;)。&amp; &lt; &gt;</span><span class="sxs-lookup"><span data-stu-id="8e9ef-312">Don't include special XML characters in the password (&amp; &lt; &gt; ;).</span></span> <span data-ttu-id="8e9ef-313">這是腳本編寫方式的限制,而不是 Azure 的限制。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-313">This is a limitation of the way the scripts were written, not a limitation of Azure.</span></span>

    <span data-ttu-id="8e9ef-314">例如,如果要建立名為「fixitdemo」的 Web 應用並使用 SQL Server 管理員密碼「Passw0rd1」,則可以輸入以下命令:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-314">For example, if you want to create a web app named "fixitdemo" and use a SQL Server administrator password of "Passw0rd1", you could enter the following command:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    <span data-ttu-id="8e9ef-315">名稱在azurewebsites.net網域中必須是唯一的,並且密碼必須滿足SQL資料庫對密碼複雜性的要求。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-315">The name must be unique in the azurewebsites.net domain, and the password must meet SQL Database requirements for password complexity.</span></span> <span data-ttu-id="8e9ef-316">(示例 Passw0rd1 確實滿足要求。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-316">(The example Passw0rd1 does meet the requirements.)</span></span>

    <span data-ttu-id="8e9ef-317">請注意,該命令以"開頭。\".</span><span class="sxs-lookup"><span data-stu-id="8e9ef-317">Note that the command begins with ".\".</span></span> <span data-ttu-id="8e9ef-318">為了説明防止惡意執行腳本,Windows PowerShell 要求您在運行文稿時提供腳本檔的完全限定路徑。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-318">To help prevent malicious execution of scripts, Windows PowerShell requires that you provide the fully qualified path to the script file when you run a script.</span></span> <span data-ttu-id="8e9ef-319">可以使用點來指示當前目錄 (")。\"或提供完全限定的路徑,例如:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-319">You can use a dot to indicate the current directory (".\") or provide the fully qualified path, such as:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    <span data-ttu-id="8e9ef-320">有關腳本的詳細資訊,請使用`Get-Help`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-320">For more information about the script, use the `Get-Help` cmdlet.</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    <span data-ttu-id="8e9ef-321">您可以使用 取得`Detailed``Full`説明 cmdlet`Parameters``Examples`的, 與 參數來篩選傳回的說明。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-321">You can use the `Detailed`, `Full`, `Parameters`, and `Examples` parameters of the Get-Help cmdlet to filter the help that is returned.</span></span>

    <span data-ttu-id="8e9ef-322">如果文本失敗或生成錯誤,例如"新建 Azure 網站:先調用集 Azure 訂閱和選擇 Azure 訂閱",則可能尚未完成 Azure PowerShell 的配置。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-322">If the script fails or generates errors, such as "New-AzureWebsite : Call Set-AzureSubscription and Select-AzureSubscription first," you might not have completed the configuration of Azure PowerShell.</span></span>

    <span data-ttu-id="8e9ef-323">文稿完成後,可以使用 Azure 管理門戶查看已創建的資源,如[「自動所有內容」](automate-everything.md)章節所示。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-323">After the script finishes, you can use the Azure Management Portal to see the resources that were created, as shown in the [Automate Everything](automate-everything.md) chapter.</span></span>
10. <span data-ttu-id="8e9ef-324">要將 FixIt 專案部署到新的 Azure 環境,請使用*Azure 網站.ps1*腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-324">To deploy the FixIt project to the new Azure environment, use the *AzureWebsite.ps1* script.</span></span> <span data-ttu-id="8e9ef-325">例如：</span><span class="sxs-lookup"><span data-stu-id="8e9ef-325">For example:</span></span>

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    <span data-ttu-id="8e9ef-326">部署完成後,瀏覽器將在 Azure 中運行修復它時打開。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-326">When deployment is done, the browser opens with Fix It running in Azure.</span></span>

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a><span data-ttu-id="8e9ef-327">對 Windows 電源外殼文稿進行故障排除</span><span class="sxs-lookup"><span data-stu-id="8e9ef-327">Troubleshooting the Windows PowerShell scripts</span></span>

<span data-ttu-id="8e9ef-328">運行這些腳本時遇到的最常見的錯誤與許可權有關。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-328">The most common errors encountered when running these scripts are related to permissions.</span></span> <span data-ttu-id="8e9ef-329">確保`Add-AzureAccount``Import-AzurePublishSettingsFile`並成功,並且將它們用於相同的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-329">Make sure that `Add-AzureAccount` and `Import-AzurePublishSettingsFile` were successful and that you used them for the same Azure subscription.</span></span> <span data-ttu-id="8e9ef-330">即使`Add-AzureAccount`成功,你也得再次運行它。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-330">Even if `Add-AzureAccount` was successful you might have to run it again.</span></span> <span data-ttu-id="8e9ef-331">添加`Add-AzureAccount`的許可權將在 12 小時內過期。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-331">The permissions added by `Add-AzureAccount` expire in 12 hours.</span></span>

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a><span data-ttu-id="8e9ef-332">物件參考未設定成物件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-332">Object reference not set to an instance of an object.</span></span>

<span data-ttu-id="8e9ef-333">如果腳本返回錯誤(如"物件引用未設置為物件的實例",這意味著 Windows PowerShell 找不到要處理的物件(這是空引用異常),請運行`Add-AzureAccount`cmdlet 並重試該腳本。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-333">If the script returns errors, such as "Object reference not set to an instance of an object," which means that Windows PowerShell can't find an object to process (this is a null reference exception), run the `Add-AzureAccount` cmdlet and try the script again.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a><span data-ttu-id="8e9ef-334">內部錯誤:伺服器遇到內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-334">InternalError: The server encountered an internal error.</span></span>

<span data-ttu-id="8e9ef-335">當`New-AzureWebsite`名稱在azurewebsites.net網域中不唯一時,cmdlet 返回內部錯誤。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-335">The `New-AzureWebsite` cmdlet returns an internal error when the name is not unique in the azurewebsites.net domain.</span></span> <span data-ttu-id="8e9ef-336">要解決錯誤,請使用名稱的其他值,該值位於*New-Azure 網站Env.ps1*的名稱參數中。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-336">To resolve the error, use a different value for the name, which is in the Name parameter of *New-AzureWebsiteEnv.ps1*.</span></span>

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a><span data-ttu-id="8e9ef-337">重新啟動文稿</span><span class="sxs-lookup"><span data-stu-id="8e9ef-337">Restarting the script</span></span>

<span data-ttu-id="8e9ef-338">如果需要重新啟動*New-Azure 網站Env.ps1*腳本,因為它在列印"腳本已完成"消息之前出現故障,則可能需要刪除腳本在停止之前創建的資源。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-338">If you need to restart the *New-AzureWebsiteEnv.ps1* script because it failed before it printed the "Script is complete" message, you might want to delete resources that the script created before it stopped.</span></span> <span data-ttu-id="8e9ef-339">例如,如果文稿已創建 ContosoFixItDemo Web 應用,並且您再次使用相同的名稱運行文稿,則該文本將失敗,因為該名稱正在使用中。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-339">For example, if the script already created the ContosoFixItDemo web app and you run the script again with the same name, the script will fail because the name is in use.</span></span>

<span data-ttu-id="8e9ef-340">要確定文稿在停止之前建立的資源,請使用以下 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-340">To determine which resources the script created before it stopped, use the following cmdlets:</span></span>

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- <span data-ttu-id="8e9ef-341">`Get-AzureSqlDatabase`: 要執行此 cmdlet,請將`Get-AzureSqlDatabase`資料庫伺服器 名稱導管到 :`Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span><span class="sxs-lookup"><span data-stu-id="8e9ef-341">`Get-AzureSqlDatabase`: To run this cmdlet, pipe the database server name to `Get-AzureSqlDatabase`:   `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`</span></span>

<span data-ttu-id="8e9ef-342">要刪除這些資源,請使用以下命令。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-342">To delete these resources, use the following commands.</span></span> <span data-ttu-id="8e9ef-343">請注意,如果刪除資料庫伺服器,則會自動刪除與伺服器關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-343">Note that if you delete the database server, you automatically delete the databases associated with the server.</span></span>

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a><span data-ttu-id="8e9ef-344">如何將具有佇列處理的應用部署到 Azure 應用服務 Web 應用和 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="8e9ef-344">How to deploy the app with queue processing to Azure App Service Web Apps and an Azure Cloud Service</span></span>

<span data-ttu-id="8e9ef-345">要啟用佇列,請確保在 MyFixIt_Web.config 檔中進行以下更改。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-345">To enable queues, make the following change in the MyFixIt\Web.config file.</span></span> <span data-ttu-id="8e9ef-346">在`appSettings`下,將`UseQueues`的值更改為「true」:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-346">Under `appSettings`, change the value of `UseQueues` to "true":</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

<span data-ttu-id="8e9ef-347">然後,將 MVC 應用程式部署到 Azure 應用服務中的 Web 應用,如[前面](#deploybase)所述。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-347">Then deploy the MVC application to an web app in Azure App Service, as described [earlier](#deploybase).</span></span>

<span data-ttu-id="8e9ef-348">接下來,創建新的 Azure 雲服務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-348">Next, create a new Azure cloud service.</span></span> <span data-ttu-id="8e9ef-349">修復 It 應用中包含的腳本不會創建或部署雲服務,因此必須為此使用 Azure 門戶。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-349">The scripts included with the Fix It app do not create or deploy the cloud service, so you must use Azure portal for this.</span></span> <span data-ttu-id="8e9ef-350">在門戶中,按下 **「新** -- **計算**+**雲端服務** -- **快速創建**」,然後輸入 URL 和資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-350">In the portal, click **New** -- **Compute** – **Cloud Service** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="8e9ef-351">使用部署 Web 應用的同一資料中心。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-351">Use the same data center where you deployed the web app.</span></span>

![](the-fix-it-sample-application/_static/image1.png)

<span data-ttu-id="8e9ef-352">在部署雲服務之前,需要更新某些配置檔。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-352">Before you can deploy the cloud service, you need to update some of the configuration files.</span></span>

<span data-ttu-id="8e9ef-353">在 MyFixIt.WorkerRole_app.config`connectionStrings`中,在`appdb`下, 將連接字串的值替換為 SQL 資料庫的實際連接字串。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-353">In MyFixIt.WorkerRole\app.config, under `connectionStrings`, replace the value of the `appdb` connection string with the actual connection string for the SQL Database.</span></span> <span data-ttu-id="8e9ef-354">可以從門戶獲取連接字串。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-354">You can get the connection string from the portal.</span></span> <span data-ttu-id="8e9ef-355">在門戶中,按一下**ADO .Net、ODBC、PHP 和 JDBC 的\*\*\*\*SQL 資料庫** - **appdb** - 檢視 SQL 資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-355">In the portal, click **SQL Databases** - **appdb** - **View SQL Database connection strings for ADO .Net, ODBC, PHP, and JDBC**.</span></span> <span data-ttu-id="8e9ef-356">複製ADO.NET連接字串並將該值貼上到app.config檔中。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-356">Copy the ADO.NET connection string and paste the value into the app.config file.</span></span> <span data-ttu-id="8e9ef-357">將「此處的\_密碼\_」替換為資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-357">Replace "{your\_password\_here}" with your database password.</span></span> <span data-ttu-id="8e9ef-358">(假設您使用腳本部署 MVC 應用,則可以在腳本`SqlDatabasePassword`參數中 指定資料庫密碼。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-358">(Assuming you used the scripts to deploy the MVC app, you specified the database password in the `SqlDatabasePassword` script parameter.)</span></span>

<span data-ttu-id="8e9ef-359">結果應如下所示:</span><span class="sxs-lookup"><span data-stu-id="8e9ef-359">The result should look like the following:</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

<span data-ttu-id="8e9ef-360">在同一 MyFixIt.WorkerRole_app.config`appSettings`檔下 ,替換 Azure 儲存帳戶的兩個占位符值。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-360">In the same MyFixIt.WorkerRole\app.config file, under `appSettings`, replace the two placeholder values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

<span data-ttu-id="8e9ef-361">可以從門戶獲取訪問密鑰。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-361">You can get the access key from the portal.</span></span> <span data-ttu-id="8e9ef-362">請參考[如何管理儲存帳號](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-362">See [How To Manage Storage Accounts](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>

<span data-ttu-id="8e9ef-363">在 MyFixItCloudService 服務配置.Cloud.cscfg 中,替換 Azure 儲存帳戶的兩個占位符值。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-363">In MyFixItCloudService\ServiceConfiguration.Cloud.cscfg, replace the same two placeholders values for the Azure storage account.</span></span>

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

<span data-ttu-id="8e9ef-364">現在,您已準備好部署雲服務。</span><span class="sxs-lookup"><span data-stu-id="8e9ef-364">Now you are ready to deploy the cloud service.</span></span> <span data-ttu-id="8e9ef-365">在「解決方案流覽」中,右鍵單擊 MyFixIt雲端服務專案並選擇 **「發布」。**</span><span class="sxs-lookup"><span data-stu-id="8e9ef-365">In Solution Explore, right-click the MyFixItCloudService project and select **Publish**.</span></span> <span data-ttu-id="8e9ef-366">有關詳細資訊,請參閱[本教程的第](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36)2 部分中的"[將應用程式部署到 Azure"。](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)</span><span class="sxs-lookup"><span data-stu-id="8e9ef-366">For more information, see "[Deploy the Application to Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz)", which is in part 2 of [this tutorial](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8e9ef-367">上一步</span><span class="sxs-lookup"><span data-stu-id="8e9ef-367">Previous</span></span>](more-patterns-and-guidance.md)
