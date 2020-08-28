---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 加入模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 453a55bd9f16c7b33525de18bc49493d22776f47
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045113"
---
# <a name="adding-a-model"></a>新增模型

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

在本節中，您將新增一些類別來管理資料庫中的電影。 這些類別將會是 &quot; &quot; ASP.NET MVC 應用程式的模型部分。

您將使用稱為 [Entity Framework](https://docs.microsoft.com/ef/) 的 .NET Framework 資料存取技術來定義和使用這些模型類別。 Entity Framework (通常稱為 EF) 支援稱為 *Code First*的開發範例。 Code First 可讓您撰寫簡單的類別來建立模型物件。  (這些也稱為 POCO 類別，來自于單純 &quot; 的 CLR 物件。 &quot;) 您接著就可以從類別即時建立資料庫，以實現非常乾淨且快速的開發工作流程。 如果您需要先建立資料庫，您仍然可以遵循本教學課程來瞭解如何開發 MVC 和 EF 應用程式。 接著，您可以遵循 Tom Fizmakens [ASP.NET](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) 樣板教學課程，其中涵蓋資料庫的第一種方法。

## <a name="adding-model-classes"></a>新增模型類別

在 **方案總管**中，以滑鼠右鍵按一下 [ *模型* ] 資料夾，選取 [ **新增**]，然後選取 [ **類別**]。

![](adding-a-model/_static/image1.png)

輸入 *類別* 名稱 &quot; 電影 &quot; 。

將下列五個屬性新增至 `Movie` 類別：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我們將使用 `Movie` 類別來代表資料庫中的電影。 物件的每個實例 `Movie` 都會對應至資料庫資料表中的資料列，而類別的每個屬性 `Movie` 都會對應到資料表中的資料行。

注意：若要使用 system.string 和相關類別，您必須安裝 [Entity Framework NuGet 套件](https://www.nuget.org/packages/EntityFramework/)。 請遵循連結以取得進一步的指示。

在相同的檔案中，新增下列 `MovieDBContext` 類別：

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`類別代表 Entity Framework movie 資料庫內容，它會處理在資料庫中提取、儲存和更新 `Movie` 類別實例的工作。 `MovieDBContext`衍生自 Entity Framework 所 `DbContext` 提供的基類。

您必須在檔案 `DbContext` `DbSet` 的最上方加入下列語句，才能夠參考和 `using` ：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

若要這麼做，您可以手動加入 using 語句，也可以將滑鼠停留在紅色的波浪線上， `Show potential fixes` 然後按一下並按一下 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注意：已移除數個未使用的 `using` 語句。 Visual Studio 將會以灰色顯示未使用的相依性。 若要移除未使用的相依性，您可以將滑鼠停留在灰色相依性上，按一下 [ `Show potential fixes` **移除未使用的 using** ]

![](adding-a-model/_static/image3.png)

我們最後在 MVC) 中加入了 (M 的模型。 在下一節中，您將會使用資料庫連接字串。

> [!div class="step-by-step"]
> [上一個](adding-a-view.md) 
> [下一步](creating-a-connection-string.md)
