---
ms.openlocfilehash: 1c342231905775938715280681ea2b4cf6ebc9bc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047935"
---
將下列屬性新增至 `Movie` 類別：

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/Movie.cs?name=snippet1)]

`Movie` 類別包含：

* `Id` 欄位，此為資料庫需要針對主索引鍵使用的必要欄位。
* `[DataType(DataType.Date)]`：[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 屬性會指定資料的類型 (`Date`)。 使用此屬性：

  * 使用者不需要在日期欄位中輸入時間資訊。
  * 只會顯示日期，不會顯示時間資訊。

稍後的教學課程會涵蓋 [DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)。