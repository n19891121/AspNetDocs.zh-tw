---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 教學課程：開始使用 EF Database First 使用 MVC 5
description: 本教學課程會示範如何開始使用的現有資料庫，並快速建立 web 應用程式，可讓使用者與資料互動。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65121168"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>教學課程：開始使用 EF Database First 使用 MVC 5

您可以使用 MVC、 Entity Framework 和 ASP.NET Scaffolding，來建立 web 應用程式，提供介面給現有的資料庫。 本系列教學課程會示範如何自動產生程式碼，可讓使用者顯示、 編輯、 建立及刪除位於資料庫資料表中的資料。 產生的程式碼會對應至資料庫資料表中的資料行。 在系列的最後一個部分中，您將了解如何將資料註解新增至資料模型，以指定驗證需求，並顯示格式設定。 當您完成時，您可以前往 Azure 的文章，以了解如何將.NET 應用程式和 SQL database 部署到 Azure App Service。

本教學課程會示範如何開始使用的現有資料庫，並快速建立 web 應用程式，可讓使用者與資料互動。 它會使用 Entity Framework 6 和 MVC 5 建置 web 應用程式。 ASP.NET 樣板功能可讓您自動產生程式碼顯示、 更新、 建立和刪除資料。 使用 Visual Studio 內發行的工具，您可以輕鬆地部署站台和資料庫至 Azure。

此系列的一部分，著重於建立資料庫，並填入資料。

此系列是以貢獻寫入，Tom Dykstra 和 Rick Anderson。 它已改善根據意見反應的註解區段中的使用者。

在本教學課程中，您已：

> [!div class="checklist"]
> * 將資料庫設定

## <a name="prerequisites"></a>必要條件

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>將資料庫設定

為了模擬的環境需要現有的資料庫，您會先使用一些預先填入的資料，建立資料庫，然後再建立 web 應用程式連接至資料庫。

本教學課程被開發使用 Visual Studio 2017 中使用 LocalDB。 您可以使用現有的資料庫伺服器，而不使用 LocalDB，但根據您的 Visual Studio 和您的資料庫類型的版本，所有的 Visual Studio 中的資料工具可能不支援。 如果工具不適用於您的資料庫中，您可能需要針對您的資料庫執行某些管理套件中的特定資料庫的步驟。

如果您的 Visual Studio 版本中有資料庫工具的問題，請確定您已安裝最新版的資料庫工具。 如需更新或安裝資料庫工具的資訊，請參閱[Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)。

啟動 Visual Studio 並建立**SQL Server 資料庫專案**。 將專案命名為**ContosoUniversityData**。

![建立資料庫專案](setting-up-database/_static/image1.png)

您現在有了空的資料庫專案。 若要確定您可以將此資料庫部署至 Azure，您會將 Azure SQL Database 作為專案的目標平台。 設定目標平台不會實際部署資料庫，例如：它只表示資料庫專案將會確認資料庫設計適用於目標平台。 若要設定目標平台，請開啟**屬性**的專案，然後選取**Microsoft Azure SQL Database**目標平台。

您可以建立本教學課程需要加上定義的資料表的 SQL 指令碼的資料表。 以滑鼠右鍵按一下您的專案，並加入新項目。 選取 **資料表和檢視表** > **表格**並將它命名*學生*。

在資料表的檔案中，取代下列程式碼來建立資料表中的 T-SQL 命令。

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

請注意，[設計] 視窗會自動同步處理的程式碼。 您可以使用程式碼或設計工具。

![顯示程式碼和設計](setting-up-database/_static/image5.png)

新增另一個資料表。 這次它命名為課程，並使用下列 T-SQL 命令。

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

然後，重複一次，建立名為註冊的資料表。

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

您可以填入您的資料庫，以透過執行指令碼會在部署資料庫之後的資料。 加入專案中的部署後指令碼。 以滑鼠右鍵按一下您的專案，並加入新項目。 選取 **使用者指令碼** > **部署後指令碼**。 您可以使用預設名稱。

將下列 T-SQL 程式碼新增至 部署後指令碼。 此指令碼只會將資料加入至資料庫，當不找到任何相符的記錄。 它不會覆寫或刪除任何您可能會在資料庫中輸入的資料。

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

請務必注意，在每次部署您的資料庫專案，執行部署後指令碼。 因此，您必須仔細考慮您的需求，撰寫這個指令碼時。 在某些情況下，您可能想要每次部署專案時，從頭開始從一組已知的資料。 在其他情況下，您可能不想變更現有的資料，以任何方式。 根據您的需求，您可以決定您是否需要部署後指令碼，或您要包含在指令碼中。 如需填入您的資料庫部署後指令碼的詳細資訊，請參閱[包括 SQL Server 資料庫專案中的資料](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。

您現在有 4 個 SQL 指令碼檔案，但沒有任何實際的資料表。 您已準備好部署至 localdb 資料庫專案。 在 Visual Studio 中，按一下 [開始] 按鈕 （或 F5），來建置及部署您的資料庫專案。 請檢查**輸出**索引標籤，以確認建置和部署是否成功。

若要查看已建立新資料庫，請開啟**SQL Server 物件總管**並尋找正確的本機資料庫伺服器中的專案名稱 (在此情況下 **(localdb) \ProjectsV13**)。

若要查看資料表會填入資料，以滑鼠右鍵按一下資料表，然後選取**檢視資料**。

![顯示資料表資料](setting-up-database/_static/image9.png)

資料表資料的可編輯檢視隨即顯示。 例如，如果您選取**資料表** > **dbo.course** > **檢視資料**，您會看到三個資料行的資料表 (**課程**， **title**，以及**信用額度**) 和四個資料列。

## <a name="additional-resources"></a>其他資源

Code First 開發簡介範例，請參閱[Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)。 如需更進階的範例，請參閱 <<c0> [ 建立 ASP.NET MVC 4 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

如需選取要使用哪個 Entity Framework 方法的指引，請參閱 < [Entity Framework 開發方式](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 將資料庫設定

請前進到下一個教學課程，以了解如何建立 web 應用程式和資料模型。
> [!div class="nextstepaction"]
> [建立 web 應用程式和資料模型](creating-the-web-application.md)
