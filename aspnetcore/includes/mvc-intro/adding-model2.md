---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044075"
---
## <a name="add-initial-migration-and-update-the-database"></a><span data-ttu-id="7cc1b-101">新增初始移轉並更新資料庫</span><span class="sxs-lookup"><span data-stu-id="7cc1b-101">Add initial migration and update the database</span></span>

* <span data-ttu-id="7cc1b-102">開啟命令提示字元並巡覽至專案目錄。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-102">Open a command prompt and navigate to the project directory.</span></span> <span data-ttu-id="7cc1b-103">(目錄包含*Startup.cs*檔案)。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-103">(The directory containing the *Startup.cs* file).</span></span>

* <span data-ttu-id="7cc1b-104">在命令提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="7cc1b-104">Run the following commands in the command prompt:</span></span>

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  <span data-ttu-id="7cc1b-105">[.NET core](/dotnet/core/tools/index)是.NET 的跨平台實作。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-105">[.NET Core](/dotnet/core/tools/index) is a cross-platform implementation of .NET.</span></span> <span data-ttu-id="7cc1b-106">以下是這些命令所執行的動作：</span><span class="sxs-lookup"><span data-stu-id="7cc1b-106">Here is what these commands do:</span></span>

  * <span data-ttu-id="7cc1b-107">[dotnet 還原](/dotnet/core/tools/dotnet-restore):下載 NuGet 套件中指定 *.csproj*檔案。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): Downloads the NuGet packages specified in the *.csproj* file.</span></span>
  * <span data-ttu-id="7cc1b-108">`dotnet ef migrations add Initial` 執行 Entity Framework 的.NET Core CLI 移轉命令，並建立初始移轉。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-108">`dotnet ef migrations add Initial` Runs the Entity Framework .NET Core CLI migrations command and creates the initial migration.</span></span> <span data-ttu-id="7cc1b-109">您指派給移轉名稱參數之後 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-109">The parameter after "add" is a name that you assign to the migration.</span></span> <span data-ttu-id="7cc1b-110">這裡您命名移轉 「 初始 」 因為它是初始資料庫移轉。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-110">Here you're naming the migration "Initial" because it's the initial database migration.</span></span> <span data-ttu-id="7cc1b-111">此作業會建立*Data/Migrations/\<日期時間 > _Initial.cs*檔案，其中包含要新增的移轉命令*電影*到資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-111">This operation creates the *Data/Migrations/\<date-time>_Initial.cs* file containing the migration commands to add the *Movie* table to the database.</span></span>
  * <span data-ttu-id="7cc1b-112">`dotnet ef database update`  使用我們剛才建立的移轉更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-112">`dotnet ef database update`  Updates the database with the migration we just created.</span></span>

<span data-ttu-id="7cc1b-113">在下一個教學課程中，您將了解的資料庫和連接字串。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-113">You'll learn about the database and connection string in the next tutorial.</span></span> <span data-ttu-id="7cc1b-114">您將了解中的資料模型變更[將欄位加入](xref:tutorials/first-mvc-app/new-field)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7cc1b-114">You'll learn about data model changes in the [Add a field](xref:tutorials/first-mvc-app/new-field) tutorial.</span></span>
