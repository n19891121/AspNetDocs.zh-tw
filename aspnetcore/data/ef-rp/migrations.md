---
title: ASP.NET Core 中的 Razor 頁面與 EF Core - 移轉 - 4/8
author: rick-anderson
description: 在本教學課程中，您將開始使用 EF Core 移轉功能來管理 ASP.NET Core MVC 應用程式中的資料模型變更。
ms.author: riande
ms.date: 6/31/2017
uid: data/ef-rp/migrations
ms.openlocfilehash: 2051f55bfa7a9582486df78ec91315f0b03cb1e8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030115"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---migrations---4-of-8"></a><span data-ttu-id="7f87c-103">ASP.NET Core 中的 Razor 頁面與 EF Core - 移轉 - 4/8</span><span class="sxs-lookup"><span data-stu-id="7f87c-103">Razor Pages with EF Core in ASP.NET Core - Migrations - 4 of 8</span></span>

[!INCLUDE[2.0 version](~/includes/RP-EF/20-pdf.md)]

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7f87c-104">作者：[Tom Dykstra](https://github.com/tdykstra)、[Jon P Smith](https://twitter.com/thereformedprog) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7f87c-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](~/includes/RP-EF/intro.md)]

<span data-ttu-id="7f87c-105">在本教學課程中，會使用 EF Core 移轉功能來管理資料模型變更。</span><span class="sxs-lookup"><span data-stu-id="7f87c-105">In this tutorial, the EF Core migrations feature for managing data model changes is used.</span></span>

<span data-ttu-id="7f87c-106">若您遇到無法解決的問題，請下載[完整應用程式](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples)。</span><span class="sxs-lookup"><span data-stu-id="7f87c-106">If you run into problems you can't solve, download the [completed app](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples).</span></span>

<span data-ttu-id="7f87c-107">開發新的應用程式時，資料模型經常變更。</span><span class="sxs-lookup"><span data-stu-id="7f87c-107">When a new app is developed, the data model changes frequently.</span></span> <span data-ttu-id="7f87c-108">每次模型變更時，模型就與資料庫不同步。</span><span class="sxs-lookup"><span data-stu-id="7f87c-108">Each time the model changes, the model gets out of sync with the database.</span></span> <span data-ttu-id="7f87c-109">本教學課程從設定 Entity Framework 來建立不存在的資料庫開始。</span><span class="sxs-lookup"><span data-stu-id="7f87c-109">This tutorial started by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="7f87c-110">每次資料模型變更時：</span><span class="sxs-lookup"><span data-stu-id="7f87c-110">Each time the data model changes:</span></span>

* <span data-ttu-id="7f87c-111">會卸除資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-111">The DB is dropped.</span></span>
* <span data-ttu-id="7f87c-112">EF 會建立一個符合模型的新資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-112">EF creates a new one that matches the model.</span></span>
* <span data-ttu-id="7f87c-113">應用程式會將測試資料植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-113">The app seeds the DB with test data.</span></span>

<span data-ttu-id="7f87c-114">在您將應用程式部署到生產環境之前，這種讓資料庫與資料模型保持同步的方法效果不錯。</span><span class="sxs-lookup"><span data-stu-id="7f87c-114">This approach to keeping the DB in sync with the data model works well until you deploy the app to production.</span></span> <span data-ttu-id="7f87c-115">當應用程式在生產環境中執行時，它通常會儲存需要維護的資料。</span><span class="sxs-lookup"><span data-stu-id="7f87c-115">When the app is running in production, it's usually storing data that needs to be maintained.</span></span> <span data-ttu-id="7f87c-116">應用程式不能每次進行變更 (例如新增資料行) 時，都從測試資料庫開始。</span><span class="sxs-lookup"><span data-stu-id="7f87c-116">The app can't start with a test DB each time a change is made (such as adding a new column).</span></span> <span data-ttu-id="7f87c-117">EF Core 移轉功能可解決這個問題，方法是啟用 EF Core 以更新資料庫結構描述，來代替建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-117">The EF Core Migrations feature solves this problem by enabling EF Core to update the DB schema instead of creating a new DB.</span></span>

<span data-ttu-id="7f87c-118">移轉會更新結構描述，並保留現有的資料，而不是在資料模型變更時，卸除並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-118">Rather than dropping and recreating the DB when the data model changes, migrations updates the schema and retains existing data.</span></span>

## <a name="drop-the-database"></a><span data-ttu-id="7f87c-119">卸除資料庫</span><span class="sxs-lookup"><span data-stu-id="7f87c-119">Drop the database</span></span>

<span data-ttu-id="7f87c-120">使用 [SQL Server 物件總管] (SSOX) 或 `database drop` 命令：</span><span class="sxs-lookup"><span data-stu-id="7f87c-120">Use **SQL Server Object Explorer** (SSOX) or the `database drop` command:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7f87c-121">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f87c-121">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="7f87c-122">在 [套件管理員主控台] (PMC) 中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7f87c-122">In the **Package Manager Console** (PMC), run the following command:</span></span>

```PMC
Drop-Database
```

<span data-ttu-id="7f87c-123">從 PMC 執行 `Get-Help about_EntityFrameworkCore` 以取得說明資訊。</span><span class="sxs-lookup"><span data-stu-id="7f87c-123">Run `Get-Help about_EntityFrameworkCore` from the PMC to get help information.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7f87c-124">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7f87c-124">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="7f87c-125">開啟命令視窗並巡覽至專案資料夾。</span><span class="sxs-lookup"><span data-stu-id="7f87c-125">Open a command window and navigate to the project folder.</span></span> <span data-ttu-id="7f87c-126">專案資料夾中包含 *Startup.cs* 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f87c-126">The project folder contains the *Startup.cs* file.</span></span>

<span data-ttu-id="7f87c-127">在命令視窗中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7f87c-127">Enter the following in the command window:</span></span>

 ```console
 dotnet ef database drop
 ```

------

## <a name="create-an-initial-migration-and-update-the-db"></a><span data-ttu-id="7f87c-128">建立初始移轉並更新資料庫</span><span class="sxs-lookup"><span data-stu-id="7f87c-128">Create an initial migration and update the DB</span></span>

<span data-ttu-id="7f87c-129">建置專案並建立第一個移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-129">Build the project and create the first migration.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7f87c-130">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f87c-130">Visual Studio</span></span>](#tab/visual-studio)

```PMC
Add-Migration InitialCreate
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7f87c-131">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7f87c-131">.NET Core CLI</span></span>](#tab/netcore-cli)

```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

------

### <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="7f87c-132">檢查 Up 和 Down 方法</span><span class="sxs-lookup"><span data-stu-id="7f87c-132">Examine the Up and Down methods</span></span>

<span data-ttu-id="7f87c-133">EF Core 命令 `migrations add` 已產生用來建立資料庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f87c-133">The EF Core `migrations add` command  generated code to create the DB.</span></span> <span data-ttu-id="7f87c-134">此移轉程式碼位於 Migrations\<時間戳記>_InitialCreate.cs 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7f87c-134">This migrations code is in the *Migrations\<timestamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="7f87c-135">`InitialCreate` 類別的 `Up` 方法會建立對應至資料模型實體集的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="7f87c-135">The `Up` method of the `InitialCreate` class creates the DB tables that correspond to the data model entity sets.</span></span> <span data-ttu-id="7f87c-136">`Down` 方法則會刪除它們，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="7f87c-136">The `Down` method deletes them, as shown in the following example:</span></span>

[!code-csharp[](intro/samples/cu21/Migrations/20180626224812_InitialCreate.cs?range=7-24,77-88)]

<span data-ttu-id="7f87c-137">移轉會呼叫 `Up` 方法，以實作資料模型變更來進行移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-137">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="7f87c-138">當您輸入命令以復原更新時，移轉會呼叫 `Down` 方法。</span><span class="sxs-lookup"><span data-stu-id="7f87c-138">When you enter a command to roll back the update, migrations calls the `Down` method.</span></span>

<span data-ttu-id="7f87c-139">上述程式碼適用於初始移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-139">The preceding code is for the initial migration.</span></span> <span data-ttu-id="7f87c-140">該程式碼是在執行 `migrations add InitialCreate` 命令時建立。</span><span class="sxs-lookup"><span data-stu-id="7f87c-140">That code was created when the `migrations add InitialCreate` command was run.</span></span> <span data-ttu-id="7f87c-141">移轉名稱參數 (在範例中為 "InitialCreate") 用於檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="7f87c-141">The migration name parameter ("InitialCreate" in the example) is used for the file name.</span></span> <span data-ttu-id="7f87c-142">移轉名稱可以是任何有效的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="7f87c-142">The migration name can be any valid file name.</span></span> <span data-ttu-id="7f87c-143">您最好選擇單字或片語來摘要列出移轉中所要完成的作業。</span><span class="sxs-lookup"><span data-stu-id="7f87c-143">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="7f87c-144">例如，新增了部門資料表的移轉可能稱為 "AddDepartmentTable"。</span><span class="sxs-lookup"><span data-stu-id="7f87c-144">For example, a migration that added a department table might be called "AddDepartmentTable."</span></span>

<span data-ttu-id="7f87c-145">如果已建立初始移轉並結束資料庫，則：</span><span class="sxs-lookup"><span data-stu-id="7f87c-145">If the initial migration is created and the DB exists:</span></span>

* <span data-ttu-id="7f87c-146">會產生資料庫建立程式碼。</span><span class="sxs-lookup"><span data-stu-id="7f87c-146">The DB creation code is generated.</span></span>
* <span data-ttu-id="7f87c-147">不需要執行資料庫建立程式碼，因為資料庫已符合資料模型。</span><span class="sxs-lookup"><span data-stu-id="7f87c-147">The DB creation code doesn't need to run because the DB already matches the data model.</span></span> <span data-ttu-id="7f87c-148">如果執行了資料庫建立程式碼，它不會進行任何變更，因為資料庫已符合資料模型。</span><span class="sxs-lookup"><span data-stu-id="7f87c-148">If the DB creation code is run, it doesn't make any changes because the DB already matches the data model.</span></span>

<span data-ttu-id="7f87c-149">當應用程式部署到新的環境時，必須執行資料庫建立程式碼來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-149">When the app is deployed to a new environment, the DB creation code must be run to create the DB.</span></span>

<span data-ttu-id="7f87c-150">先前資料庫已卸除，並不存在，所以移轉會建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-150">Previously the DB was dropped and doesn't exist, so migrations creates the new DB.</span></span>

### <a name="the-data-model-snapshot"></a><span data-ttu-id="7f87c-151">資料模型快照集</span><span class="sxs-lookup"><span data-stu-id="7f87c-151">The data model snapshot</span></span>

<span data-ttu-id="7f87c-152">移轉會在 *Migrations/SchoolContextModelSnapshot.cs* 中建立目前資料庫結構描述的「快照」。</span><span class="sxs-lookup"><span data-stu-id="7f87c-152">Migrations create a *snapshot* of the current database schema in *Migrations/SchoolContextModelSnapshot.cs*.</span></span> <span data-ttu-id="7f87c-153">當您新增移轉時，EF 會比較資料模型與快照集檔案，以判斷變更的內容。</span><span class="sxs-lookup"><span data-stu-id="7f87c-153">When you add a migration, EF determines what changed by comparing the data model to the snapshot file.</span></span>

<span data-ttu-id="7f87c-154">若要刪除移轉，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="7f87c-154">To delete a migration, use the following command:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="7f87c-155">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7f87c-155">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="7f87c-156">Remove-Migration</span><span class="sxs-lookup"><span data-stu-id="7f87c-156">Remove-Migration</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="7f87c-157">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="7f87c-157">.NET Core CLI</span></span>](#tab/netcore-cli)

```console
dotnet ef migrations remove
```

<span data-ttu-id="7f87c-158">如需詳細資訊，請參閱 [dotnet ef migrations remove](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove)。</span><span class="sxs-lookup"><span data-stu-id="7f87c-158">For more information, see  [dotnet ef migrations remove](/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove).</span></span>

------

<span data-ttu-id="7f87c-159">remove migrations 命令會刪除移轉，並確保正確地重設快照集。</span><span class="sxs-lookup"><span data-stu-id="7f87c-159">The remove migrations command deletes the migration and ensures the snapshot is correctly reset.</span></span>

### <a name="remove-ensurecreated-and-test-the-app"></a><span data-ttu-id="7f87c-160">移除 EnsureCreated 並測試應用程式</span><span class="sxs-lookup"><span data-stu-id="7f87c-160">Remove EnsureCreated and test the app</span></span>

<span data-ttu-id="7f87c-161">早期開發會使用 `EnsureCreated`。</span><span class="sxs-lookup"><span data-stu-id="7f87c-161">For early development, `EnsureCreated` was used.</span></span> <span data-ttu-id="7f87c-162">在本教學課程中，則使用移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-162">In this tutorial, migrations are used.</span></span> <span data-ttu-id="7f87c-163">`EnsureCreated` 具有下列限制：</span><span class="sxs-lookup"><span data-stu-id="7f87c-163">`EnsureCreated` has the following limitations:</span></span>

* <span data-ttu-id="7f87c-164">略過移轉，並建立資料庫和結構描述。</span><span class="sxs-lookup"><span data-stu-id="7f87c-164">Bypasses migrations and creates the DB and schema.</span></span>
* <span data-ttu-id="7f87c-165">不會建立移轉資料表。</span><span class="sxs-lookup"><span data-stu-id="7f87c-165">Doesn't create a migrations table.</span></span>
* <span data-ttu-id="7f87c-166">「無法」與移轉搭配使用。</span><span class="sxs-lookup"><span data-stu-id="7f87c-166">Can *not* be used with migrations.</span></span>
* <span data-ttu-id="7f87c-167">設計用來測試或快速原型化經常卸除並重新建立資料庫的位置。</span><span class="sxs-lookup"><span data-stu-id="7f87c-167">Is designed for testing or rapid prototyping where the DB is dropped and re-created frequently.</span></span>

<span data-ttu-id="7f87c-168">從 `DbInitializer` 移除下列各行：</span><span class="sxs-lookup"><span data-stu-id="7f87c-168">Remove the following line from `DbInitializer`:</span></span>

```csharp
context.Database.EnsureCreated();
```

<span data-ttu-id="7f87c-169">執行應用程式，並確認植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-169">Run the app and verify the DB is seeded.</span></span>

### <a name="inspect-the-database"></a><span data-ttu-id="7f87c-170">檢查資料庫</span><span class="sxs-lookup"><span data-stu-id="7f87c-170">Inspect the database</span></span>

<span data-ttu-id="7f87c-171">使用 **SQL Server 物件總管**來檢查資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-171">Use **SQL Server Object Explorer** to inspect the DB.</span></span> <span data-ttu-id="7f87c-172">請注意已新增 `__EFMigrationsHistory` 資料表。</span><span class="sxs-lookup"><span data-stu-id="7f87c-172">Notice the addition of an `__EFMigrationsHistory` table.</span></span> <span data-ttu-id="7f87c-173">`__EFMigrationsHistory` 資料表會追蹤哪些移轉經套用至資料庫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-173">The `__EFMigrationsHistory` table keeps track of which migrations have been applied to the DB.</span></span> <span data-ttu-id="7f87c-174">檢視 `__EFMigrationsHistory` 資料表中的資料，它會顯示第一個移轉的某個資料列。</span><span class="sxs-lookup"><span data-stu-id="7f87c-174">View the data in the `__EFMigrationsHistory` table, it shows one row for the first migration.</span></span> <span data-ttu-id="7f87c-175">上述 CLI 輸出範例中的最後一則記錄會顯示建立此資料列的 INSERT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7f87c-175">The last log in the preceding CLI output example shows the INSERT statement that creates this row.</span></span>

<span data-ttu-id="7f87c-176">執行應用程式，並確認一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="7f87c-176">Run the app and verify that everything works.</span></span>

## <a name="applying-migrations-in-production"></a><span data-ttu-id="7f87c-177">在生產環境中套用移轉</span><span class="sxs-lookup"><span data-stu-id="7f87c-177">Applying migrations in production</span></span>

<span data-ttu-id="7f87c-178">建議在應用程式啟動時，生產環境應用程式**不**應該呼叫 [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)。</span><span class="sxs-lookup"><span data-stu-id="7f87c-178">We recommend production apps should **not** call [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) at application startup.</span></span> <span data-ttu-id="7f87c-179">`Migrate` 不應該從伺服器陣列中的應用程式進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="7f87c-179">`Migrate` shouldn't be called from an app in server farm.</span></span> <span data-ttu-id="7f87c-180">例如，如果應用程式已使用向外延展 (執行應用程式的多個執行個體) 進行雲端部署。</span><span class="sxs-lookup"><span data-stu-id="7f87c-180">For example, if the app has been cloud deployed with scale-out (multiple instances of the app are running).</span></span>

<span data-ttu-id="7f87c-181">資料庫移轉應該在部署中以受控制的方式完成。</span><span class="sxs-lookup"><span data-stu-id="7f87c-181">Database migration should be done as part of deployment, and in a controlled way.</span></span> <span data-ttu-id="7f87c-182">生產環境資料庫移轉方法包括：</span><span class="sxs-lookup"><span data-stu-id="7f87c-182">Production database migration approaches include:</span></span>

* <span data-ttu-id="7f87c-183">使用移轉來建立 SQL 指令碼，並在部署中使用 SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7f87c-183">Using migrations to create SQL scripts and using the SQL scripts in deployment.</span></span>
* <span data-ttu-id="7f87c-184">從受控制的環境中執行 `dotnet ef database update`。</span><span class="sxs-lookup"><span data-stu-id="7f87c-184">Running `dotnet ef database update` from a controlled environment.</span></span>

<span data-ttu-id="7f87c-185">EF Core 使用 `__MigrationsHistory` 資料表來查看是否有任何需要執行的移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-185">EF Core uses the `__MigrationsHistory` table to see if any migrations need to run.</span></span> <span data-ttu-id="7f87c-186">如果資料庫為最新狀態，則不會執行移轉。</span><span class="sxs-lookup"><span data-stu-id="7f87c-186">If the DB is up-to-date, no migration is run.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7f87c-187">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7f87c-187">Troubleshooting</span></span>

<span data-ttu-id="7f87c-188">下載[完整應用程式](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)。</span><span class="sxs-lookup"><span data-stu-id="7f87c-188">Download the [completed app](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="7f87c-189">應用程式會產生下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="7f87c-189">The app generates the following exception:</span></span>

```text
SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

<span data-ttu-id="7f87c-190">解決方案:執行 `dotnet ef database update`</span><span class="sxs-lookup"><span data-stu-id="7f87c-190">Solution: Run `dotnet ef database update`</span></span>

### <a name="additional-resources"></a><span data-ttu-id="7f87c-191">其他資源</span><span class="sxs-lookup"><span data-stu-id="7f87c-191">Additional resources</span></span>

* <span data-ttu-id="7f87c-192">[.NET Core CLI](/ef/core/miscellaneous/cli/dotnet)。</span><span class="sxs-lookup"><span data-stu-id="7f87c-192">[.NET Core CLI](/ef/core/miscellaneous/cli/dotnet).</span></span>
* [<span data-ttu-id="7f87c-193">套件管理員主控台 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7f87c-193">Package Manager Console (Visual Studio)</span></span>](/ef/core/miscellaneous/cli/powershell)

::: moniker-end

> [!div class="step-by-step"]
> <span data-ttu-id="7f87c-194">[上一頁](xref:data/ef-rp/sort-filter-page)
> [下一頁](xref:data/ef-rp/complex-data-model)</span><span class="sxs-lookup"><span data-stu-id="7f87c-194">[Previous](xref:data/ef-rp/sort-filter-page)
[Next](xref:data/ef-rp/complex-data-model)</span></span>
