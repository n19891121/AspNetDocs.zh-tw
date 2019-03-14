---
ms.openlocfilehash: 72e33ea44976963193d2560427fc418875be450e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038865"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="73563-101">新增模型到 ASP.NET Core MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="73563-101">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="73563-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 與 [Ryan Nowak](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="73563-102">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="73563-103">在本節中，您將新增一些類別來管理資料庫中的電影。</span><span class="sxs-lookup"><span data-stu-id="73563-103">In this section, you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="73563-104">這些類別是 **MVC** 應用程式的「模型」部分。</span><span class="sxs-lookup"><span data-stu-id="73563-104">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="73563-105">搭配 [Entity Framework Core](/ef/core) (EF Core) 使用這些類別，即可使用資料庫。</span><span class="sxs-lookup"><span data-stu-id="73563-105">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="73563-106">EF Core 是一種物件關聯式對應 (ORM) 架構，可簡化您必須撰寫的資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="73563-106">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span> <span data-ttu-id="73563-107">[EF Core 支援許多資料庫引擎](/ef/core/providers/)。</span><span class="sxs-lookup"><span data-stu-id="73563-107">[EF Core supports many database engines](/ef/core/providers/).</span></span>

<span data-ttu-id="73563-108">您所建立的模型類別稱為 POCO 類別 (來自「純舊 CLR 物件」)，因為它們對 EF Core 沒有任何相依性。</span><span class="sxs-lookup"><span data-stu-id="73563-108">The model classes you'll create are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="73563-109">它們只會定義資料庫將儲存之資料的屬性。</span><span class="sxs-lookup"><span data-stu-id="73563-109">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="73563-110">在本教學課程中，您首先要撰寫模型類別，而 EF Core 將建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="73563-110">In this tutorial you'll write the model classes first, and EF Core will create the database.</span></span> <span data-ttu-id="73563-111">本文未提及的替代方法是從現有的資料庫產生模型類別。</span><span class="sxs-lookup"><span data-stu-id="73563-111">An alternate approach not covered here is to generate model classes from an already-existing database.</span></span> <span data-ttu-id="73563-112">如需該方法的資訊，請參閱 [ASP.NET Core - 現有的資料庫](/ef/core/get-started/aspnetcore/existing-db)。</span><span class="sxs-lookup"><span data-stu-id="73563-112">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="73563-113">新增資料模型類別</span><span class="sxs-lookup"><span data-stu-id="73563-113">Add a data model class</span></span>
