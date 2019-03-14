---
ms.openlocfilehash: e098ad497b13b4add583de017885cdbed952a421
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036755"
---
<!-- This include not used by windows version -->
# <a name="add-a-new-field-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="ab4d8-101">將欄位新增至 ASP.NET Core MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="ab4d8-101">Add a new field to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="ab4d8-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="ab4d8-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="ab4d8-103">本教學課程會將新欄位新增至 `Movies` 資料表。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-103">This tutorial will add a new field to the `Movies` table.</span></span> <span data-ttu-id="ab4d8-104">我們會在變更結構描述 (新增欄位) 時，卸除資料庫並建立一個新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-104">We'll drop the database and create a new one when we change the schema (add a new field).</span></span> <span data-ttu-id="ab4d8-105">在開發早期我們不需要保存任何生產環境資料時，這個工作流程可正常運作。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-105">This workflow works well early in development when we don't have any production data to perserve.</span></span>

<span data-ttu-id="ab4d8-106">一旦部署了應用程式，而且有需要保存的資料後，在需要變更結構描述時就無法卸除資料庫。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-106">Once your app is deployed and you have data that you need to perserve, you can't drop your DB when you need to change the schema.</span></span> <span data-ttu-id="ab4d8-107">Entity Framework [Code First 移轉](/ef/core/get-started/aspnetcore/new-db)可讓您更新結構描述並移轉資料庫，而不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-107">Entity Framework [Code First Migrations](/ef/core/get-started/aspnetcore/new-db) allows you to update your schema and migrate the database without losing data.</span></span> <span data-ttu-id="ab4d8-108">移轉是使用 SQL Server 時常用的功能，但 SQLlite 不支援許多移轉結構描述作業，因此只能執行移轉。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-108">Migrations is a popular feature when using SQL Server, but SQLlite doesn't support many migration schema operations, so only very simply migrations are possible.</span></span> <span data-ttu-id="ab4d8-109">如需詳細資訊，請參閱 [SQLite 限制](/ef/core/providers/sqlite/limitations)。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-109">See [SQLite Limitations](/ef/core/providers/sqlite/limitations) for more information.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="ab4d8-110">將 Rating 屬性新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="ab4d8-110">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="ab4d8-111">開啟 *Models/Movie.cs* 檔案，然後新增 `Rating` 屬性：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-111">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Models/MovieDateRating.cs?highlight=12&name=snippet)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

::: moniker-end

<span data-ttu-id="ab4d8-112">因為您已將新欄位新增至 `Movie` 類別，所以也需要更新繫結白名單，以便包含這個新屬性。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-112">Because you've added a new field to the `Movie` class, you also need to update the binding whitelist so this new property will be included.</span></span> <span data-ttu-id="ab4d8-113">在 *MoviesController.cs* 中，更新 `Create` 和 `Edit` 這兩個動作方法的 `[Bind]` 屬性 (attribute)，以包括 `Rating` 屬性 (property)：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-113">In *MoviesController.cs*, update the `[Bind]` attribute for both the `Create` and `Edit` action methods to include the `Rating` property:</span></span>

```csharp
[Bind("ID,Title,ReleaseDate,Genre,Price,Rating")]
   ```

<span data-ttu-id="ab4d8-114">您也需要更新檢視範本，以便在瀏覽器檢視中顯示、建立和編輯新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-114">You also need to update the view templates in order to display, create, and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="ab4d8-115">編輯 */Views/Movies/Index.cshtml* 檔案，然後新增 `Rating` 欄位：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-115">Edit the */Views/Movies/Index.cshtml* file and add a `Rating` field:</span></span>

[!code-HTML[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexGenreRating.cshtml?highlight=17,39&range=24-64)]

<span data-ttu-id="ab4d8-116">使用 `Rating` 欄位更新 */Views/Movies/Create.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-116">Update the */Views/Movies/Create.cshtml* with a `Rating` field.</span></span>

<span data-ttu-id="ab4d8-117">在我們更新資料庫以包含新欄位之前，應用程式無法運作。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-117">The app won't work until we update the DB to include the new field.</span></span> <span data-ttu-id="ab4d8-118">如果您立即執行應用程式，則會收到下列 `SqliteException`：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-118">If you run it now, you'll get the following `SqliteException`:</span></span>

```
SqliteException: SQLite Error 1: 'no such column: m.Rating'.
```

<span data-ttu-id="ab4d8-119">您看到此錯誤是因為更新的電影模型類別，不同於現有資料庫之電影資料表的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-119">You're seeing this error because the updated Movie model class is different than the schema of the Movie table of the existing database.</span></span> <span data-ttu-id="ab4d8-120">(資料庫資料表中沒有任何 `Rating` 資料行)。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-120">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="ab4d8-121">有幾個方法可以解決這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-121">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="ab4d8-122">卸除資料庫，並且讓 Entity Framework 自動重新建立以新的模型類別結構描述為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-122">Drop the database and have the Entity Framework automatically re-create the database based on the new model class schema.</span></span> <span data-ttu-id="ab4d8-123">使用此方法時，您會遺失資料庫中的現有資料，因此不能對生產環境資料庫執行此操作！</span><span class="sxs-lookup"><span data-stu-id="ab4d8-123">With this approach, you lose existing data in the database — so you can't do this with a production database!</span></span> <span data-ttu-id="ab4d8-124">使用初始設定式將測試資料自動植入資料庫，通常是開發應用程式的有效方式。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-124">Using an initializer to automatically seed a database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="ab4d8-125">以手動方式修改現有資料庫的結構描述，使其符合模型類別。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-125">Manually modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="ab4d8-126">這種方法的優點是可以保留您的資料。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-126">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="ab4d8-127">您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-127">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="ab4d8-128">使用 Code First 移轉來更新資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-128">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="ab4d8-129">在此教學課程中，當結構描述變更時，我們將卸除並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-129">For this tutorial, we'll drop and re-create the database when the schema changes.</span></span> <span data-ttu-id="ab4d8-130">從終端機中執行下列命令，以卸除資料庫：</span><span class="sxs-lookup"><span data-stu-id="ab4d8-130">Run the following command from a terminal to drop the db:</span></span>

`dotnet ef database drop`

<span data-ttu-id="ab4d8-131">更新 `SeedData` 類別，使其提供新資料行的值。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-131">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="ab4d8-132">範例變更如下所示，但您會想要為每個 `new Movie` 進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-132">A sample change is shown below, but you'll want to make this change for each `new Movie`.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/SeedDataRating.cs?name=snippet1&highlight=6)]

<span data-ttu-id="ab4d8-133">將 `Rating` 欄位新增至 `Edit`、`Details` 和 `Delete` 檢視。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-133">Add the `Rating` field to the `Edit`, `Details`, and `Delete` view.</span></span>

<span data-ttu-id="ab4d8-134">執行應用程式，並確認您可以使用 `Rating` 欄位建立/編輯/顯示電影。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-134">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="ab4d8-135">範本。</span><span class="sxs-lookup"><span data-stu-id="ab4d8-135">templates.</span></span>
