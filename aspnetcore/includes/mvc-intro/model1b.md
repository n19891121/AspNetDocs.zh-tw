---
ms.openlocfilehash: 1c342231905775938715280681ea2b4cf6ebc9bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047935"
---
<span data-ttu-id="6e1e0-101">將下列屬性新增至 `Movie` 類別：</span><span class="sxs-lookup"><span data-stu-id="6e1e0-101">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="6e1e0-102">`Movie` 類別包含：</span><span class="sxs-lookup"><span data-stu-id="6e1e0-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="6e1e0-103">`Id` 欄位，此為資料庫需要針對主索引鍵使用的必要欄位。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-103">The `Id` field which is required by the database for the primary key.</span></span>
* <span data-ttu-id="6e1e0-104">`[DataType(DataType.Date)]`：[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 屬性會指定資料的類型 (`Date`)。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (`Date`).</span></span> <span data-ttu-id="6e1e0-105">使用此屬性：</span><span class="sxs-lookup"><span data-stu-id="6e1e0-105">With this attribute:</span></span>

  * <span data-ttu-id="6e1e0-106">使用者不需要在日期欄位中輸入時間資訊。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="6e1e0-107">只會顯示日期，不會顯示時間資訊。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="6e1e0-108">稍後的教學課程會涵蓋 [DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)。</span><span class="sxs-lookup"><span data-stu-id="6e1e0-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>