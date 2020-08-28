---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 建立連接字串以及使用 SQL Server LocalDB |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 4400cb8c6a5d57da60d164220f929d69d7f4d2f7
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044255"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>建立連接字串以及使用 SQL Server LocalDB

依 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](~/includes/razor.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>建立連接字串以及使用 SQL Server LocalDB

`MovieDBContext`您所建立的類別會處理連接至資料庫的工作，並將 `Movie` 物件對應至資料庫記錄。 不過，您可能會問的一個問題是如何指定要連接的資料庫。 您實際上不需要指定要使用的資料庫，Entity Framework 將預設為使用 [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。 在本節中，我們會在應用程式的 *Web.config* 檔中明確地新增連接字串。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) 是 SQL Server Express 資料庫引擎的輕量版本，可依需求啟動並以使用者模式執行。 LocalDB 是在 SQL Server Express 的特殊執行模式中執行，可讓您使用資料庫做為 *.mdf* 檔。 LocalDB 資料庫檔案通常會保留在 Web 專案的 *應用程式 \_ 資料* 資料夾中。

不建議在生產環境 web 應用程式中使用 SQL Server Express。 由於 LocalDB 並非設計用來與 IIS 搭配運作，因此不應該用於生產環境與 web 應用程式。 不過，您可以輕鬆地將 LocalDB 資料庫移轉至 SQL Server 或 SQL Azure。

在 Visual Studio 2017 中，預設會使用 Visual Studio 安裝 LocalDB。

根據預設，Entity Framework 會尋找與這個專案) 之物件內容類別 (名稱相同的連接字串 `MovieDBContext` 。 如需詳細資訊，請參閱 [SQL Server ASP.NET Web 應用程式的連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。

開啟應用程式根目錄 *Web.config* 檔，如下所示。  (不是*Views*資料夾中的*Web.config*檔案。 ) 

![](creating-a-connection-string/_static/image1.png)

尋找 `<connectionStrings>` 元素：

![](creating-a-connection-string/_static/image2.png)

將下列連接字串新增至 `<connectionStrings>` *Web.config* 檔案中的元素。

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

下列範例會顯示已新增連接字串的部分 *Web.config* 檔案：

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

這兩個連接字串非常類似。 第一個連接字串會命名為 `DefaultConnection` ，並用於成員資格資料庫，以控制誰可以存取應用程式。 您已新增的連接字串會指定名為 *Movie* 的 LocalDB 資料庫（位於 *應用程式 \_ 資料* 資料夾中）。 本教學課程不會使用成員資格資料庫，如需成員資格、驗證和安全性的詳細資訊，請參閱我的教學課程 [如何使用驗證和 SQL DB 建立 ASP.NET MVC 應用程式，並部署至 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。

連接字串的名稱必須與 [DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 類別的名稱相符。

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

您實際上不需要加入 `MovieDBContext` 連接字串。 如果您未指定連接字串，Entity Framework 將會在使用者目錄中建立具有 [DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 類別完整名稱的 LocalDB 資料庫， (在此情況下 `MvcMovie.Models.MovieDBContext`) 。 您可以將資料庫命名為任何您喜歡的名稱，前提是它具有 *。MDF* 尾碼。 例如，我們可以將資料庫命名為 *MyFilms .mdf*。

接下來，您將建立新的 `MoviesController` 類別，讓您可以用來顯示電影資料，並允許使用者建立新的電影清單。

> [!div class="step-by-step"]
> [上一個](adding-a-model.md) 
> [下一步](accessing-your-models-data-from-a-controller.md)
