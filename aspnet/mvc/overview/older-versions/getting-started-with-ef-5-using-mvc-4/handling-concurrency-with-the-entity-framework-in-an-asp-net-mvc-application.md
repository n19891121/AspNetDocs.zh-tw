---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中處理 Entity Framework 的並行處理， (7/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b7d6ff8d6de27ee0935bc9cb8cc053efb8751d4b
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985707"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a><span data-ttu-id="278fe-103">在 ASP.NET MVC 應用程式中處理 Entity Framework 的並行處理， (7/10) </span><span class="sxs-lookup"><span data-stu-id="278fe-103">Handling Concurrency with the Entity Framework in an ASP.NET MVC Application (7 of 10)</span></span>

<span data-ttu-id="278fe-104">由 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="278fe-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="278fe-105">Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="278fe-105">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="278fe-106">如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="278fe-106">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="278fe-107">如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。</span><span class="sxs-lookup"><span data-stu-id="278fe-107">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="278fe-108">您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。</span><span class="sxs-lookup"><span data-stu-id="278fe-108">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="278fe-109">針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。</span><span class="sxs-lookup"><span data-stu-id="278fe-109">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>

<span data-ttu-id="278fe-110">在先前的兩個教學課程中，您使用了相關的資料。</span><span class="sxs-lookup"><span data-stu-id="278fe-110">In the previous two tutorials you worked with related data.</span></span> <span data-ttu-id="278fe-111">本教學課程說明如何處理並行。</span><span class="sxs-lookup"><span data-stu-id="278fe-111">This tutorial shows how to handle concurrency.</span></span> <span data-ttu-id="278fe-112">您將建立可與實體搭配使用的網頁 `Department` ，而編輯和刪除實體的頁面 `Department` 將會處理並行錯誤。</span><span class="sxs-lookup"><span data-stu-id="278fe-112">You'll create web pages that work with the `Department` entity, and the pages that edit and delete `Department` entities will handle concurrency errors.</span></span> <span data-ttu-id="278fe-113">下圖顯示 [索引] 和 [刪除] 頁面，包括發生並行衝突時所顯示的一些訊息。</span><span class="sxs-lookup"><span data-stu-id="278fe-113">The following illustrations show the Index and Delete pages, including some messages that are displayed if a concurrency conflict occurs.</span></span>

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a><span data-ttu-id="278fe-116">並行衝突</span><span class="sxs-lookup"><span data-stu-id="278fe-116">Concurrency Conflicts</span></span>

<span data-ttu-id="278fe-117">當一名使用者為了編輯而顯示了實體的資料，然後另一名使用者在第一名使用者所作出的變更寫入到資料庫前便更新了相同實體的資料時，便會發生並行衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-117">A concurrency conflict occurs when one user displays an entity's data in order to edit it, and then another user updates the same entity's data before the first user's change is written to the database.</span></span> <span data-ttu-id="278fe-118">若您沒有啟用針對這類衝突的偵測，最後更新資料庫的使用者所作出的變更便會覆寫前一名使用者所作出的變更。</span><span class="sxs-lookup"><span data-stu-id="278fe-118">If you don't enable the detection of such conflicts, whoever updates the database last overwrites the other user's changes.</span></span> <span data-ttu-id="278fe-119">在許多應用程式中，這類風險是可接受的：若僅有幾名使用者或僅有幾項更新，或覆寫變更的風險並不是那麼的重大，則為了處理並行而耗費的程式設計成本可能會大於其所能帶來的利益。</span><span class="sxs-lookup"><span data-stu-id="278fe-119">In many applications, this risk is acceptable: if there are few users, or few updates, or if isn't really critical if some changes are overwritten, the cost of programming for concurrency might outweigh the benefit.</span></span> <span data-ttu-id="278fe-120">在此情況下，您便不需要設定應用程式來處理並行衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-120">In that case, you don't have to configure the application to handle concurrency conflicts.</span></span>

### <a name="pessimistic-concurrency-locking"></a><span data-ttu-id="278fe-121">封閉式平行存取 (鎖定) </span><span class="sxs-lookup"><span data-stu-id="278fe-121">Pessimistic Concurrency (Locking)</span></span>

<span data-ttu-id="278fe-122">若您的應用程式確實需要防止在並行案例下發生的意外資料遺失，其中一個方法便是使用資料庫鎖定。</span><span class="sxs-lookup"><span data-stu-id="278fe-122">If your application does need to prevent accidental data loss in concurrency scenarios, one way to do that is to use database locks.</span></span> <span data-ttu-id="278fe-123">這稱為封閉式 *並行* 存取。</span><span class="sxs-lookup"><span data-stu-id="278fe-123">This is called *pessimistic concurrency*.</span></span> <span data-ttu-id="278fe-124">例如，在您從資料庫讀取一個資料列之前，您會要求唯讀鎖定或更新存取鎖定。</span><span class="sxs-lookup"><span data-stu-id="278fe-124">For example, before you read a row from a database, you request a lock for read-only or for update access.</span></span> <span data-ttu-id="278fe-125">若您鎖定了一個資料列以進行更新存取，其他使用者便無法為了唯讀或更新存取而鎖定該資料列，因為他們會取得一個正在進行變更之資料的複本。</span><span class="sxs-lookup"><span data-stu-id="278fe-125">If you lock a row for update access, no other users are allowed to lock the row either for read-only or update access, because they would get a copy of data that's in the process of being changed.</span></span> <span data-ttu-id="278fe-126">若您鎖定資料列以進行唯讀存取，其他使用者也可以為了唯讀存取將其鎖定，但無法進行更新。</span><span class="sxs-lookup"><span data-stu-id="278fe-126">If you lock a row for read-only access, others can also lock it for read-only access but not for update.</span></span>

<span data-ttu-id="278fe-127">管理鎖定有幾個缺點。</span><span class="sxs-lookup"><span data-stu-id="278fe-127">Managing locks has disadvantages.</span></span> <span data-ttu-id="278fe-128">其程式可能相當複雜。</span><span class="sxs-lookup"><span data-stu-id="278fe-128">It can be complex to program.</span></span> <span data-ttu-id="278fe-129">它需要大量的資料庫管理資源，而且可能會造成效能問題，因為應用程式的使用者數目增加 (也就是說，它不會) 調整。</span><span class="sxs-lookup"><span data-stu-id="278fe-129">It requires significant database management resources, and it can cause performance problems as the number of users of an application increases (that is, it doesn't scale well).</span></span> <span data-ttu-id="278fe-130">基於這些理由，不是所有的資料庫管理系統都支援封閉式並行存取。</span><span class="sxs-lookup"><span data-stu-id="278fe-130">For these reasons, not all database management systems support pessimistic concurrency.</span></span> <span data-ttu-id="278fe-131">Entity Framework 不提供任何內建的支援，而且本教學課程不會示範如何執行。</span><span class="sxs-lookup"><span data-stu-id="278fe-131">The Entity Framework provides no built-in support for it, and this tutorial doesn't show you how to implement it.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="278fe-132">開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="278fe-132">Optimistic Concurrency</span></span>

<span data-ttu-id="278fe-133">封閉式平行存取的替代方式是 *開放式並行* 存取。</span><span class="sxs-lookup"><span data-stu-id="278fe-133">The alternative to pessimistic concurrency is *optimistic concurrency*.</span></span> <span data-ttu-id="278fe-134">開放式並行存取表示允許並行衝突發生，然後在衝突發生時適當的做出反應。</span><span class="sxs-lookup"><span data-stu-id="278fe-134">Optimistic concurrency means allowing concurrency conflicts to happen, and then reacting appropriately if they do.</span></span> <span data-ttu-id="278fe-135">例如，John 執行部門編輯頁面，將英文部門的 **預算** 金額從 $350000.00 變更為 $0.00。</span><span class="sxs-lookup"><span data-stu-id="278fe-135">For example, John runs the Departments Edit page, changes the **Budget** amount for the English department from $350,000.00 to $0.00.</span></span>

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="278fe-137">在 John 按一下 [ **儲存**] 之前，Jane 執行相同的頁面，並將 [ **開始日期** ] 欄位從9/1/2007 變更為8/8/2013。</span><span class="sxs-lookup"><span data-stu-id="278fe-137">Before John clicks **Save**, Jane runs the same page and changes the **Start Date** field from 9/1/2007 to 8/8/2013.</span></span>

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="278fe-139">John 先按下 [ **儲存** ]，並在瀏覽器返回 [索引] 頁面時看到其變更，然後按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="278fe-139">John clicks **Save** first and sees his change when the browser returns to the Index page, then Jane clicks **Save**.</span></span> <span data-ttu-id="278fe-140">接下來發生的情況便是由您處理並行衝突的方式決定。</span><span class="sxs-lookup"><span data-stu-id="278fe-140">What happens next is determined by how you handle concurrency conflicts.</span></span> <span data-ttu-id="278fe-141">一部分選項包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="278fe-141">Some of the options include the following:</span></span>

- <span data-ttu-id="278fe-142">您可以追蹤使用者修改的屬性，然後僅在資料庫中更新相對應的資料行。</span><span class="sxs-lookup"><span data-stu-id="278fe-142">You can keep track of which property a user has modified and update only the corresponding columns in the database.</span></span> <span data-ttu-id="278fe-143">在範例案例中，將不會發生資料遺失，因為兩名使用者更新的屬性不同。</span><span class="sxs-lookup"><span data-stu-id="278fe-143">In the example scenario, no data would be lost, because different properties were updated by the two users.</span></span> <span data-ttu-id="278fe-144">下次有人流覽英文部門時，他們就會看到 John 和 Jane 的變更，也就是開始日期為8/8/2013，預算為零元。</span><span class="sxs-lookup"><span data-stu-id="278fe-144">The next time someone browses the English department, they'll see both John's and Jane's changes — a start date of 8/8/2013 and a budget of Zero dollars.</span></span>

    <span data-ttu-id="278fe-145">這個更新方法可減少可能導致資料遺失之衝突發生的次數，但卻無法在實體中的相同屬性遭到變更時避免資料遺失。</span><span class="sxs-lookup"><span data-stu-id="278fe-145">This method of updating can reduce the number of conflicts that could result in data loss, but it can't avoid data loss if competing changes are made to the same property of an entity.</span></span> <span data-ttu-id="278fe-146">Entity Framework 是否會以這種方式處理並行衝突，取決於您實作更新程式碼的方式。</span><span class="sxs-lookup"><span data-stu-id="278fe-146">Whether the Entity Framework works this way depends on how you implement your update code.</span></span> <span data-ttu-id="278fe-147">通常在 Web 應用程式中，這種方法並不實用，因為它需要您維持大量的狀態，以追蹤實體所有原始的屬性值和新的值。</span><span class="sxs-lookup"><span data-stu-id="278fe-147">It's often not practical in a web application, because it can require that you maintain large amounts of state in order to keep track of all original property values for an entity as well as new values.</span></span> <span data-ttu-id="278fe-148">維護大量的狀態可能會影響應用程式效能，因為它需要伺服器資源或必須包含在網頁本身 (例如，在隱藏的欄位) 中。</span><span class="sxs-lookup"><span data-stu-id="278fe-148">Maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself (for example, in hidden fields).</span></span>
- <span data-ttu-id="278fe-149">您可以讓 Jane 的變更覆寫 John 的變更。</span><span class="sxs-lookup"><span data-stu-id="278fe-149">You can let Jane's change overwrite John's change.</span></span> <span data-ttu-id="278fe-150">下次有人流覽英文部門時，就會看到8/8/2013 和還原的 $350000.00 值。</span><span class="sxs-lookup"><span data-stu-id="278fe-150">The next time someone browses the English department, they'll see 8/8/2013 and the restored $350,000.00 value.</span></span> <span data-ttu-id="278fe-151">這稱之為「用戶端獲勝 (Client Wins)」或「最後寫入為準 (Last in Wins)」案例。</span><span class="sxs-lookup"><span data-stu-id="278fe-151">This is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="278fe-152"> (用戶端的值會優先于資料存放區中的內容。 ) 如本節簡介所述，如果您沒有針對並行處理進行任何編碼，則會自動發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="278fe-152">(The client's values take precedence over what's in the data store.) As noted in the introduction to this section, if you don't do any coding for concurrency handling, this will happen automatically.</span></span>
- <span data-ttu-id="278fe-153">您可以防止 Jane 的變更在資料庫中更新。</span><span class="sxs-lookup"><span data-stu-id="278fe-153">You can prevent Jane's change from being updated in the database.</span></span> <span data-ttu-id="278fe-154">一般而言，您會顯示錯誤訊息、顯示資料的目前狀態，並允許她重新套用她的變更（如果她仍想要進行變更）。</span><span class="sxs-lookup"><span data-stu-id="278fe-154">Typically, you would display an error message, show her the current state of the data, and allow her to reapply her changes if she still wants to make them.</span></span> <span data-ttu-id="278fe-155">這稱為「存放區獲勝 (Store Wins)」案例。</span><span class="sxs-lookup"><span data-stu-id="278fe-155">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="278fe-156"> (資料存放區值的優先順序高於用戶端所提交的值。 ) 您將在本教學課程中實行 Store 獲勝案例。</span><span class="sxs-lookup"><span data-stu-id="278fe-156">(The data-store values take precedence over the values submitted by the client.) You'll implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="278fe-157">這個方法可確保沒有任何變更會在使用者收到警示，告知其發生的事情前遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="278fe-157">This method ensures that no changes are overwritten without a user being alerted to what's happening.</span></span>

### <a name="detecting-concurrency-conflicts"></a><span data-ttu-id="278fe-158">偵測並行衝突</span><span class="sxs-lookup"><span data-stu-id="278fe-158">Detecting Concurrency Conflicts</span></span>

<span data-ttu-id="278fe-159">您可以藉由處理 Entity Framework 擲回的 [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) 例外狀況來解決衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-159">You can resolve conflicts by handling [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) exceptions that the Entity Framework throws.</span></span> <span data-ttu-id="278fe-160">若要得知何時應擲回這些例外狀況，Entity Framework 必須能夠偵測衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-160">In order to know when to throw these exceptions, the Entity Framework must be able to detect conflicts.</span></span> <span data-ttu-id="278fe-161">因此，您必須適當的設定資料庫及資料模型。</span><span class="sxs-lookup"><span data-stu-id="278fe-161">Therefore, you must configure the database and the data model appropriately.</span></span> <span data-ttu-id="278fe-162">一部分啟用衝突偵測的選項包括下列選項：</span><span class="sxs-lookup"><span data-stu-id="278fe-162">Some options for enabling conflict detection include the following:</span></span>

- <span data-ttu-id="278fe-163">在資料庫資料表中，包含一個追蹤資料行，該資料行可用於決定資料列發生變更的時機。</span><span class="sxs-lookup"><span data-stu-id="278fe-163">In the database table, include a tracking column that can be used to determine when a row has been changed.</span></span> <span data-ttu-id="278fe-164">然後，您可以將 Entity Framework 設定為在 `Where` SQL 或命令的子句中包含該資料行 `Update` `Delete` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-164">You can then configure the Entity Framework to include that column in the `Where` clause of SQL `Update` or `Delete` commands.</span></span>

    <span data-ttu-id="278fe-165">追蹤資料行的資料類型通常是 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="278fe-165">The data type of the tracking column is typically [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx).</span></span> <span data-ttu-id="278fe-166">[Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)值是每次更新資料列時遞增的連續數位。</span><span class="sxs-lookup"><span data-stu-id="278fe-166">The [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) value is a sequential number that's incremented each time the row is updated.</span></span> <span data-ttu-id="278fe-167">在 `Update` 或 `Delete` 命令中，子句會 `Where` 包含追蹤資料行的原始值， (原始資料列版本) 。</span><span class="sxs-lookup"><span data-stu-id="278fe-167">In an `Update` or `Delete` command, the `Where` clause includes the original value of the tracking column (the original row version).</span></span> <span data-ttu-id="278fe-168">如果正在更新的資料列已由另一位使用者變更，則資料行中的值 `rowversion` 會與原始的值不同，因此 `Update` 或 `Delete` 語句因為子句而找不到要更新的資料列 `Where` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-168">If the row being updated has been changed by another user, the value in the `rowversion` column is different than the original value, so the `Update` or `Delete` statement can't find the row to update because of the `Where` clause.</span></span> <span data-ttu-id="278fe-169">當 Entity Framework 發現或命令未更新任何資料列時 `Update` `Delete` (也就是說，當受影響的資料列數目為零) 時，它會將其解釋為並行衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-169">When the Entity Framework finds that no rows have been updated by the `Update` or `Delete` command (that is, when the number of affected rows is zero), it interprets that as a concurrency conflict.</span></span>
- <span data-ttu-id="278fe-170">將 Entity Framework 設定為在和命令的子句中包含資料表中每個資料行的原始值 `Where` `Update` `Delete` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-170">Configure the Entity Framework to include the original values of every column in the table in the `Where` clause of `Update` and `Delete` commands.</span></span>

    <span data-ttu-id="278fe-171">在第一個選項中，如果在第一次讀取資料列之後，資料列中的任何資料都有所變更，則 `Where` 子句不會傳回要更新的資料列，而 Entity Framework 會將其解釋為並行衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-171">As in the first option, if anything in the row has changed since the row was first read, the `Where` clause won't return a row to update, which the Entity Framework interprets as a concurrency conflict.</span></span> <span data-ttu-id="278fe-172">對於具有許多資料行的資料庫資料表，此方法可能會產生非常大 `Where` 的子句，而且可能需要您維持大量的狀態。</span><span class="sxs-lookup"><span data-stu-id="278fe-172">For database tables that have many columns, this approach can result in very large `Where` clauses, and can require that you maintain large amounts of state.</span></span> <span data-ttu-id="278fe-173">如先前所述，維護大量的狀態可能會影響應用程式效能，因為它可能需要伺服器資源或必須包含在網頁本身中。</span><span class="sxs-lookup"><span data-stu-id="278fe-173">As noted earlier, maintaining large amounts of state can affect application performance because it either requires server resources or must be included in the web page itself.</span></span> <span data-ttu-id="278fe-174">因此，通常不建議使用這種方法，而且它不是本教學課程中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="278fe-174">Therefore this approach generally not recommended, and it isn't the method used in this tutorial.</span></span>

    <span data-ttu-id="278fe-175">如果您想要將這種方法實作為平行存取，您必須將 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) 屬性新增至其中，以標示您想要追蹤平行存取之實體中的所有非主要索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="278fe-175">If you do want to implement this approach to concurrency, you have to mark all non-primary-key properties in the entity you want to track concurrency for by adding the [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) attribute to them.</span></span> <span data-ttu-id="278fe-176">這項變更可讓 Entity Framework 在語句的 SQL 子句中包含所有資料行 `WHERE` `UPDATE` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-176">That change enables the Entity Framework to include all columns in the SQL `WHERE` clause of `UPDATE` statements.</span></span>

<span data-ttu-id="278fe-177">在本教學課程的其餘部分，您會將 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 追蹤屬性新增至 `Department` 實體、建立控制器和視圖，並進行測試以確認一切都正常運作。</span><span class="sxs-lookup"><span data-stu-id="278fe-177">In the remainder of this tutorial you'll add a [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tracking property to the `Department` entity, create a controller and views, and test to verify that everything works correctly.</span></span>

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a><span data-ttu-id="278fe-178">將開放式平行存取屬性新增至部門實體</span><span class="sxs-lookup"><span data-stu-id="278fe-178">Add an Optimistic Concurrency Property to the Department Entity</span></span>

<span data-ttu-id="278fe-179">在 *Models\Department.cs* 中，新增名為的追蹤屬性 `RowVersion` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-179">In *Models\Department.cs*, add a tracking property named `RowVersion`:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

<span data-ttu-id="278fe-180">[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)屬性指定這個資料行將包含在 `Where` `Update` 傳送至資料庫的子句和 `Delete` 命令中。</span><span class="sxs-lookup"><span data-stu-id="278fe-180">The [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) attribute specifies that this column will be included in the `Where` clause of `Update` and `Delete` commands sent to the database.</span></span> <span data-ttu-id="278fe-181">因為先前版本的 SQL Server 在 SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)取代它之前使用 sql[時間戳記](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx)資料類型，所以屬性稱為[時間戳記](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="278fe-181">The attribute is called [Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) because previous versions of SQL Server used a SQL [timestamp](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) data type before the SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) replaced it.</span></span> <span data-ttu-id="278fe-182">的 .Net 型別 `rowversion` 是位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="278fe-182">The .Net type for `rowversion` is a byte array.</span></span> <span data-ttu-id="278fe-183">如果您想要使用流暢的 API，您可以使用 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) 方法來指定追蹤屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="278fe-183">If you prefer to use the fluent API, you can use the [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) method to specify the tracking property, as shown in the following example:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="278fe-184">請參閱 GitHub 問題 [Replace IsConcurrencyToken By IsRowVersion](https://github.com/dotnet/AspNetDocs/issues/302)。</span><span class="sxs-lookup"><span data-stu-id="278fe-184">See the GitHub issue [Replace IsConcurrencyToken by IsRowVersion](https://github.com/dotnet/AspNetDocs/issues/302).</span></span>

<span data-ttu-id="278fe-185">由於新增屬性之後，您也變更了資料庫模型，因此您必須再一次進行移轉。</span><span class="sxs-lookup"><span data-stu-id="278fe-185">By adding a property you changed the database model, so you need to do another migration.</span></span> <span data-ttu-id="278fe-186">請在套件管理員主控台 (PMC) 中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="278fe-186">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a><span data-ttu-id="278fe-187">建立部門控制器</span><span class="sxs-lookup"><span data-stu-id="278fe-187">Create a Department Controller</span></span>

<span data-ttu-id="278fe-188">`Department`使用下列設定，以與其他控制器相同的方式來建立控制器和 views：</span><span class="sxs-lookup"><span data-stu-id="278fe-188">Create a `Department` controller and views the same way you did the other controllers, using the following settings:</span></span>

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

<span data-ttu-id="278fe-190">在 *Controllers\DepartmentController.cs* 中，新增 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="278fe-190">In *Controllers\DepartmentController.cs*, add a `using` statement:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="278fe-191">將此檔案中任何位置的 "LastName" 變更為 "FullName" (四次出現) 如此一來，[部門系統管理員] 下拉式清單將會包含講師的完整名稱，而不是 [姓氏]。</span><span class="sxs-lookup"><span data-stu-id="278fe-191">Change "LastName" to "FullName" everywhere in this file (four occurrences) so that the department administrator drop-down lists will contain the full name of the instructor rather than just the last name.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

<span data-ttu-id="278fe-192">以下列程式碼取代方法的現有程式碼 `HttpPost` `Edit` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-192">Replace the existing code for the `HttpPost` `Edit` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

<span data-ttu-id="278fe-193">視圖會將原始值儲存 `RowVersion` 在隱藏欄位中。</span><span class="sxs-lookup"><span data-stu-id="278fe-193">The view will store the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="278fe-194">當模型系結器建立 `department` 實例時，該物件會有原始的 `RowVersion` 屬性值和其他屬性的新值，如使用者在 [編輯] 頁面上輸入的。</span><span class="sxs-lookup"><span data-stu-id="278fe-194">When the model binder creates the `department` instance, that object will have the original `RowVersion` property value and the new values for the other properties, as entered by the user on the Edit page.</span></span> <span data-ttu-id="278fe-195">然後當 Entity Framework 建立 SQL 命令時 `UPDATE` ，該命令將會包含一個 `WHERE` 子句，以尋找具有原始值的資料列 `RowVersion` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-195">Then when the Entity Framework creates a SQL `UPDATE` command, that command will include a `WHERE` clause that looks for a row that has the original `RowVersion` value.</span></span>

<span data-ttu-id="278fe-196">如果命令未影響任何資料列 `UPDATE` (沒有任何資料列) 的原始 `RowVersion` 值，則 Entity Framework 會擲回 `DbUpdateConcurrencyException` 例外狀況，而區塊中的程式碼會 `catch` 從例外狀況物件中取得受影響的 `Department` 實體。</span><span class="sxs-lookup"><span data-stu-id="278fe-196">If no rows are affected by the `UPDATE` command (no rows have the original `RowVersion` value), the Entity Framework throws a `DbUpdateConcurrencyException` exception, and the code in the `catch` block gets the affected `Department` entity from the exception object.</span></span> <span data-ttu-id="278fe-197">此實體具有從資料庫讀取的值，以及使用者輸入的新值：</span><span class="sxs-lookup"><span data-stu-id="278fe-197">This entity has both the values read from the database and the new values entered by the user:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="278fe-198">接下來，程式碼會為每個資料行加入自訂錯誤訊息，而該資料行的資料庫值與使用者在 [編輯] 頁面上輸入的不同。</span><span class="sxs-lookup"><span data-stu-id="278fe-198">Next, the code adds a custom error message for each column that has database values different from what the user entered on the Edit page:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="278fe-199">較長的錯誤訊息會說明發生了什麼事，以及該怎麼做呢：</span><span class="sxs-lookup"><span data-stu-id="278fe-199">A longer error message explains what happened and what to do about it:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="278fe-200">最後，程式碼會將 `RowVersion` 物件的值設定 `Department` 為從資料庫抓取的新值。</span><span class="sxs-lookup"><span data-stu-id="278fe-200">Finally, the code sets the `RowVersion` value of the `Department` object to the new value retrieved from the database.</span></span> <span data-ttu-id="278fe-201">這個新的 `RowVersion` 值會在編輯頁面重新顯示時儲存於隱藏欄位中，並且當下一次使用者按一下 [儲存] 時，只有在重新顯示 [編輯] 頁面之後發生的並行錯誤才會被捕捉到。</span><span class="sxs-lookup"><span data-stu-id="278fe-201">This new `RowVersion` value will be stored in the hidden field when the Edit page is redisplayed, and the next time the user clicks **Save**, only concurrency errors that happen since the redisplay of the Edit page will be caught.</span></span>

<span data-ttu-id="278fe-202">在 [ *Views\Department\Edit.cshtml*] 中，加入隱藏的欄位來儲存 `RowVersion` 屬性值，緊接著屬性的隱藏欄位之後 `DepartmentID` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-202">In *Views\Department\Edit.cshtml*, add a hidden field to save the `RowVersion` property value, immediately following the hidden field for the `DepartmentID` property:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

<span data-ttu-id="278fe-203">在 *Views\Department\Index.cshtml* 中，以下列程式碼取代現有的程式碼，將資料列連結移至左邊，並變更頁面標題和資料行標題以顯示 `FullName` 而不是 `LastName` 在 **系統管理員** 欄位中：</span><span class="sxs-lookup"><span data-stu-id="278fe-203">In *Views\Department\Index.cshtml*, replace the existing code with the following code to move row links to the left and change the page title and column headings to display `FullName` instead of `LastName` in the **Administrator** column:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a><span data-ttu-id="278fe-204">測試開放式平行存取處理</span><span class="sxs-lookup"><span data-stu-id="278fe-204">Testing Optimistic Concurrency Handling</span></span>

<span data-ttu-id="278fe-205">執行網站並按一下 [ **部門**]：</span><span class="sxs-lookup"><span data-stu-id="278fe-205">Run the site and click **Departments**:</span></span>

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="278fe-207">以滑鼠右鍵按一下 [Abercrombie] 的 [ **編輯** ] 超連結，並選取 [在新索引標籤 **中開啟]，** 然後按一下 [Kim Abercrombie 的 **編輯** 超連結</span><span class="sxs-lookup"><span data-stu-id="278fe-207">Right click the **Edit** hyperlink for Kim Abercrombie and select **Open in new tab,** then click the **Edit** hyperlink for Kim Abercrombie.</span></span> <span data-ttu-id="278fe-208">這兩個視窗會顯示相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="278fe-208">The two windows display the same information.</span></span>

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="278fe-210">變更第一個瀏覽器視窗中的欄位，然後按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="278fe-210">Change a field in the first browser window and click **Save**.</span></span>

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="278fe-212">瀏覽器會顯示索引頁面，當中包含了變更之後的值。</span><span class="sxs-lookup"><span data-stu-id="278fe-212">The browser shows the Index page with the changed value.</span></span>

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="278fe-214">變更第二個瀏覽器視窗中的 [任何] 欄位，然後按一下 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="278fe-214">Change the any field in the second browser window and click **Save**.</span></span>

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="278fe-216">在第二個瀏覽器視窗中，按一下 [ **儲存** ]。</span><span class="sxs-lookup"><span data-stu-id="278fe-216">Click **Save** in the second browser window.</span></span> <span data-ttu-id="278fe-217">您會看到一個錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="278fe-217">You see an error message:</span></span>

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="278fe-219">再按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="278fe-219">Click **Save** again.</span></span> <span data-ttu-id="278fe-220">您在第二個瀏覽器中輸入的值會與您在第一個瀏覽器中變更之資料的原始值一起儲存。</span><span class="sxs-lookup"><span data-stu-id="278fe-220">The value you entered in the second browser is saved along with the original value of the data you change in the first browser.</span></span> <span data-ttu-id="278fe-221">您會在索引頁面出現時看到儲存的值。</span><span class="sxs-lookup"><span data-stu-id="278fe-221">You see the saved values when the Index page appears.</span></span>

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a><span data-ttu-id="278fe-223">更新 [刪除] 頁面</span><span class="sxs-lookup"><span data-stu-id="278fe-223">Updating the Delete Page</span></span>

<span data-ttu-id="278fe-224">針對 [刪除] 頁面，Entity Framework 會偵測由其他對部門進行類似編輯的人員所造成的並行衝突。</span><span class="sxs-lookup"><span data-stu-id="278fe-224">For the Delete page, the Entity Framework detects concurrency conflicts caused by someone else editing the department in a similar manner.</span></span> <span data-ttu-id="278fe-225">當 `HttpGet` `Delete` 方法顯示確認視圖時，此視圖會 `RowVersion` 在隱藏欄位中包含原始值。</span><span class="sxs-lookup"><span data-stu-id="278fe-225">When the `HttpGet` `Delete` method displays the confirmation view, the view includes the original `RowVersion` value in a hidden field.</span></span> <span data-ttu-id="278fe-226">該值接著可供 `HttpPost` `Delete` 使用者確認刪除時呼叫的方法使用。</span><span class="sxs-lookup"><span data-stu-id="278fe-226">That value is then available to the `HttpPost` `Delete` method that's called when the user confirms the deletion.</span></span> <span data-ttu-id="278fe-227">當 Entity Framework 建立 SQL 命令時 `DELETE` ，它會包含一個 `WHERE` 具有原始值的子句 `RowVersion` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-227">When the Entity Framework creates the SQL `DELETE` command, it includes a `WHERE` clause with the original `RowVersion` value.</span></span> <span data-ttu-id="278fe-228">如果命令導致零個數據列受到影響 (表示在) 顯示刪除確認頁面之後變更資料列，則會擲回並行例外狀況，並 `HttpGet Delete` 使用設定為的錯誤旗標來呼叫方法，以便重新 `true` 顯示包含錯誤訊息的確認頁面。</span><span class="sxs-lookup"><span data-stu-id="278fe-228">If the command results in zero rows affected (meaning the row was changed after the Delete confirmation page was displayed), a concurrency exception is thrown, and the `HttpGet Delete` method is called with an error flag set to `true` in order to redisplay the confirmation page with an error message.</span></span> <span data-ttu-id="278fe-229">由於資料列已由另一位使用者刪除，因此也可能會影響零個數據列，因此在此情況下，會顯示不同的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="278fe-229">It's also possible that zero rows were affected because the row was deleted by another user, so in that case a different error message is displayed.</span></span>

<span data-ttu-id="278fe-230">在 *DepartmentController.cs* 中，以 `HttpGet` `Delete` 下列程式碼取代方法：</span><span class="sxs-lookup"><span data-stu-id="278fe-230">In *DepartmentController.cs*, replace the `HttpGet` `Delete` method with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

<span data-ttu-id="278fe-231">方法會接受一個選用的參數，該參數會指示頁面是否已在發生並行錯誤之後重新顯示。</span><span class="sxs-lookup"><span data-stu-id="278fe-231">The method accepts an optional parameter that indicates whether the page is being redisplayed after a concurrency error.</span></span> <span data-ttu-id="278fe-232">如果此旗標為 `true` ，則會使用屬性將錯誤訊息傳送至視圖 `ViewBag` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-232">If this flag is `true`, an error message is sent to the view using a `ViewBag` property.</span></span>

<span data-ttu-id="278fe-233">`HttpPost` `Delete` 以下列程式碼取代 (命名) 方法中的程式碼 `DeleteConfirmed` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-233">Replace the code in the `HttpPost` `Delete` method (named `DeleteConfirmed`) with the following code:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="278fe-234">在您剛剛取代的 Scaffold 程式碼中，此方法僅會接受一個記錄識別碼：</span><span class="sxs-lookup"><span data-stu-id="278fe-234">In the scaffolded code that you just replaced, this method accepted only a record ID:</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="278fe-235">您已將此參數變更為模型系結器所 `Department` 建立的實體實例。</span><span class="sxs-lookup"><span data-stu-id="278fe-235">You've changed this parameter to a `Department` entity instance created by the model binder.</span></span> <span data-ttu-id="278fe-236">這可讓您存取 [ `RowVersion` 記錄] 索引鍵以外的屬性值。</span><span class="sxs-lookup"><span data-stu-id="278fe-236">This gives you access to the `RowVersion` property value in addition to the record key.</span></span>

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="278fe-237">您也將動作方法的名稱從 `DeleteConfirmed` 變更為 `Delete`。</span><span class="sxs-lookup"><span data-stu-id="278fe-237">You have also changed the action method name from `DeleteConfirmed` to `Delete`.</span></span> <span data-ttu-id="278fe-238">名為方法的 scaffold 程式碼， `HttpPost` `Delete` `DeleteConfirmed` 讓 `HttpPost` 方法成為唯一的簽章。</span><span class="sxs-lookup"><span data-stu-id="278fe-238">The scaffolded code named the `HttpPost` `Delete` method `DeleteConfirmed` to give the `HttpPost` method a unique signature.</span></span> <span data-ttu-id="278fe-239"> (CLR 要求多載方法必須有不同的方法參數。 ) 簽章是唯一的，您可以堅持使用 MVC 慣例，並針對 `HttpPost` 和 delete 方法使用相同的名稱 `HttpGet` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-239">(The CLR requires overloaded methods to have different method parameters.) Now that the signatures are unique, you can stick with the MVC convention and use the same name for the `HttpPost` and `HttpGet` delete methods.</span></span>

<span data-ttu-id="278fe-240">若捕捉到並行錯誤，程式碼會重新顯示刪除確認頁面，並提供一個旗標指示其應顯示並行錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="278fe-240">If a concurrency error is caught, the code redisplays the Delete confirmation page and provides a flag that indicates it should display a concurrency error message.</span></span>

<span data-ttu-id="278fe-241">在 *Views\Department\Delete.cshtml* 中，以下列程式碼取代 scaffold 程式碼，以進行某些格式變更並新增錯誤訊息欄位。</span><span class="sxs-lookup"><span data-stu-id="278fe-241">In *Views\Department\Delete.cshtml*, replace the scaffolded code with the following code that makes some formatting changes and adds an error message field.</span></span> <span data-ttu-id="278fe-242">所做的變更已醒目提示。</span><span class="sxs-lookup"><span data-stu-id="278fe-242">The changes are highlighted.</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

<span data-ttu-id="278fe-243">此程式碼會在和標題之間新增錯誤訊息 `h2` `h3` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-243">This code adds an error message between the `h2` and `h3` headings:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

<span data-ttu-id="278fe-244">它會 `LastName` `FullName` 在欄位中取代為 `Administrator` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-244">It replaces `LastName` with `FullName` in the `Administrator` field:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

<span data-ttu-id="278fe-245">最後，它會在語句之後，為和屬性加入隱藏的欄位 `DepartmentID` `RowVersion` `Html.BeginForm` ：</span><span class="sxs-lookup"><span data-stu-id="278fe-245">Finally, it adds hidden fields for the `DepartmentID` and `RowVersion` properties after the `Html.BeginForm` statement:</span></span>

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

<span data-ttu-id="278fe-246">執行 [部門索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="278fe-246">Run the Departments Index page.</span></span> <span data-ttu-id="278fe-247">以滑鼠右鍵按一下英文部門的 [ **刪除** ] 超連結，然後選取 [ **在新視窗中開啟]，** 然後在第一個視窗中，按一下 [英文] 部門的 [ **編輯** ] 超連結。</span><span class="sxs-lookup"><span data-stu-id="278fe-247">Right click the **Delete** hyperlink for the English department and select **Open in new window,** then in the first window click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="278fe-248">在第一個視窗中，變更其中一個值，然後按一下 [ **儲存** ]：</span><span class="sxs-lookup"><span data-stu-id="278fe-248">In the first window, change one of the values, and click **Save** :</span></span>

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="278fe-250">[索引] 頁面會確認變更。</span><span class="sxs-lookup"><span data-stu-id="278fe-250">The Index page confirms the change.</span></span>

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="278fe-252">在第二個視窗中，按一下 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="278fe-252">In the second window, click **Delete**.</span></span>

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="278fe-254">您會看到並行錯誤訊息，並且 Department 值已根據資料庫中的內容重新整理。</span><span class="sxs-lookup"><span data-stu-id="278fe-254">You see the concurrency error message, and the Department values are refreshed with what's currently in the database.</span></span>

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

<span data-ttu-id="278fe-256">若您再按一下 [刪除]，則您將會重新導向至 [索引] 頁面，並且系統將顯示該部門已遭刪除。</span><span class="sxs-lookup"><span data-stu-id="278fe-256">If you click **Delete** again, you're redirected to the Index page, which shows that the department has been deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="278fe-257">摘要</span><span class="sxs-lookup"><span data-stu-id="278fe-257">Summary</span></span>

<span data-ttu-id="278fe-258">如此即完成了處理並行衝突的簡介。</span><span class="sxs-lookup"><span data-stu-id="278fe-258">This completes the introduction to handling concurrency conflicts.</span></span> <span data-ttu-id="278fe-259">如需處理各種平行存取案例之其他方式的詳細資訊，請參閱 [開放式平行存取模式](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) ，以及使用 Entity Framework team blog 上的 [屬性值](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="278fe-259">For information about other ways to handle various concurrency scenarios, see [Optimistic Concurrency Patterns](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) and [Working with Property Values](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) on the Entity Framework team blog.</span></span> <span data-ttu-id="278fe-260">下一個教學課程將說明如何針對和實體，執行每個階層的資料表繼承 `Instructor` `Student` 。</span><span class="sxs-lookup"><span data-stu-id="278fe-260">The next tutorial shows how to implement table-per-hierarchy inheritance for the `Instructor` and `Student` entities.</span></span>

<span data-ttu-id="278fe-261">您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="278fe-261">Links to other Entity Framework resources can be found in the [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="278fe-262">[上一個](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="278fe-262">[Previous](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
