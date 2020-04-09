---
uid: whitepapers/aspnet-data-access-content-map
title: ASP.NET資料存取 - 推薦資源 |微軟文件
author: rick-anderson
description: 本主題提供指向文件資源的連結,瞭解如何存取ASP.NET Web 應用程式中的數據,主要是透過使用實體架構和 SQL Se...
ms.author: riande
ms.date: 07/25/2013
ms.assetid: f8157be1-4ab9-469e-ad3a-0ccc80b56c00
msc.legacyurl: /whitepapers/aspnet-data-access-content-map
msc.type: content
ms.openlocfilehash: 357851f195bf233c7c34a32bd156e4408d3e1b24
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676164"
---
# <a name="aspnet-data-access---recommended-resources"></a>ASP.NET 資料存取 - 建議資源

> 本主題提供指向文件資源的連結,瞭解如何存取ASP.NET Web 應用程式中的數據,主要是透過使用實體架構和SQL Server。
> 
> 如果您知道一個偉大的部落格文章,[堆疊溢出](http://stackoverflow.com)線程,或任何其他連結將有用,[給我們發一封電子郵件](mailto:aspnetue@microsoft.com?subject=Data Access Content Map)與連結。
> 
> 最後更新 4/3/2014

此主題包括下列各節：

- [ASP.NET 開始使用資料存取](#gettingstarted)
- [使用實體框架](#ef)

    - [首先使用實體框架代碼](#cf)
    - [使用實體框架代碼首次移轉](#efcfmigrations)
    - [首先使用實體框架資料庫或模型(EF 設計器)](#efdbf)
    - [在實體框架中載入相關資料(延遲載入、熱切載入和顯式載入)](#efrelateddata)
    - [優化實體框架效能](#optimizingef)
    - [在實體框架應用程式處理並發性](#efconcurrency)
    - [有關實體框架的書籍](#efbooks)
    - [其他實體框架資源](#otherefresources)
- [ASP.NET Web 表單應用程式中的資料繫結](#wfdatabinding)

    - [使用 Web 表單模型繫結](#wfmodelbinding)
    - [使用 Web 表單資料來源控制項](#wfdsc)
    - [使用 Web 表單資料繫結件和資料繫結式](#wfdbc)
- [使用 SQL 伺服器資料庫](#sqlserver)

    - [使用 SQL 伺服器快速本地資料庫](#sslocaldb)
    - [使用 SQL 伺服器快速資料庫](#sse)
    - [使用 Windows Azure SQL 資料庫](#ssdb)
    - [在 SQL 伺服器與 Windows Azure SQL 資料庫之間進行選擇](#ssdbchoosing)
- [使用 NoSQL 資料庫管理系統](#nosql)
- [在ASP.NET應用程式中使用 LINQ 查詢](#linq)
- [使用動態資料基架](#dd)
- [保護資料存取](#securing)
- [優化資料存取效能](#optimizingdataaccess)
- [部署資料庫](#deploying)
- [透過 Web 服務存取資料](#webservice)
- [其他資源](#additional)

<a id="gettingstarted"></a>

## <a name="getting-started-with-data-access-in-aspnet"></a>ASP.NET 開始使用資料存取

- [數據存儲選項(使用 Windows Azure 構建真實世界的雲端應用)。](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md) 關於雲開發電子書的章節。 引入 NoSQL 資料庫作為許多熟悉關係資料庫的開發人員傾向於忽視的替代方法。 介紹在選擇關係或 NoSQL 或選擇特定平臺時要考慮的準則。
- [ASP.NET資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx)(MSDN)。 關係資料庫的資料存取選項簡介,用於ASP.NET以及如何選擇適合您的方案的平臺和存取方法。
- [關聯資料庫](http://en.wikipedia.org/wiki/Relational_database) 維琪百科)。 如果您尚未使用關係資料庫,請參閱此頁面,瞭解關係資料庫術語和概念的介紹。 有關 SQL Server 的簡介,請參閱本主題後面使用[SQL Server 資料庫](#sqlserver)。

<a id="ef"></a>

## <a name="using-the-entity-framework"></a>使用實體框架

- [實體框架開發方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)(MSDN)。 有關如何選擇實體框架開發方法資料庫優先、模型優先或代碼優先的指導。

<a id="cf"></a>

### <a name="using-entity-framework-code-first"></a>首先使用實體框架代碼

以下教學提供可下載的範例應用程式:

- [使用 MVC 5 開始使用 EF 6。](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 涵蓋各種實體框架代碼優先方案,包括遷移和 EF 6 功能,如連接恢復能力、命令攔截和非同步。 這是[EF 5 / MVC 4 系列的](../mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)更新版本。 前面的系列包括有關新系列中未包括的存儲庫和工作單位模式的教程。
- [ASP.NET MVC 5](../mvc/overview/getting-started/introduction/getting-started.md)簡介 。 涵蓋實體框架代碼優先方案的範圍較窄,但採用更全面的工作來引入 MVC 功能。
- [模型繫結與 Web 窗體](https://go.microsoft.com/fwlink/?LinkId=286117)。 在 Web 窗體應用程式中首先使用代碼。
- [開始使用ASP.NET 4.5 Web 表單](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 Web 表單簡介,其中介紹了代碼優先。 使用模型綁定。
- [MVC音樂商店](../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1.md)。 在電子商務 MVC 3 應用程式中使用代碼優先,該應用程式還實現了成員資格和授權。 此處使用的 MVC 版本和 ASP.NET 成員資格(身份驗證和授權)系統已過時;有關ASP.NET成員資格的更多最新資訊,請參閱[https://asp.net/identity](https://asp.net/identity)。

其他資源：

- [實體框架 ─程式碼將檔案到現有資料庫](https://msdn.microsoft.com/data/jj200620)。 Msdn。 視頻和演練,演示如何將代碼優先用於現有資料庫。
- [資料開發人員中心 ─實體架構](https://msdn.microsoft.com/data/ef)。 Msdn。 有關實體框架團隊創建和維護的實體框架文檔的指南,請參閱[入門](https://msdn.microsoft.com/data/ee712907)連結。

請參閱本主題後面的[有關實體框架](#efbooks)[和其他實體框架資源](#otherefresources)的書籍。

<a id="efcfmigrations"></a>

### <a name="using-entity-framework-code-first-migrations"></a>使用實體框架代碼首次移轉

上面列出的大多數代碼第一教程都涵蓋了遷移。 另請參閱以下資源。

- [使用 Visual Studio 的 ASP.NET Web 部署](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 由兩部分組成的教程系列,演示如何使用代碼優先遷移來部署資料庫。
- [將具有成員資格、OAuth 和 SQL 資料庫的安全 ASP.NET MVC 5 應用部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 微軟 Azure)。 如何使用遷移將成員身份和應用程式數據部署到 Azure。
- [視覺化工作室與ASP.NET的 Web 部署概述](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment)。 有關代碼優先遷移如何整合到可視化工作室 Web 部署功能的說明,請參閱**可視化工作室中的「配置資料庫部署**」部分。
- [數據開發人員中心 - 代碼優先遷移](https://msdn.microsoft.com/data/jj591621)(MSDN)。 實體框架團隊的遷移文檔。
- [移至截屏廣播系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。 EF 博客)。 關於代碼優先遷移中高級主題的三個視頻。
- [使用ASP.NET網站進行代碼優先移轉](http://www.mikesdotnetting.com/Article/217/Code-First-Migrations-With-ASP.NET-Web-Pages-Sites)。 邁克斯多特網博客)。 演示如何通過將數據上下文放在 Visual Studio 類庫專案中,將代碼優先遷移與ASP.NET Web Pages 網站結合使用。

<a id="efdbf"></a>

### <a name="using-entity-framework-database-first-or-model-first-the-ef-designer"></a>首先使用實體框架資料庫或模型(EF 設計器)

- [首先使用 MVC 5 開始使用實體框架 6 資料庫](../mvc/overview/getting-started/database-first-development/setting-up-database.md)。 在伺服器資源管理器中運行文稿以創建資料庫,然後使用實體框架設計器創建數據模型。 展示如何建立簡單的 CRUD 網頁,以及對於其他資料處理功能,您可以遵循程式碼優先教學之一,因為所有 EF 工作流都使用相同的 DbContext API。

以下資源較舊。 如果要使用實體框架的版本 4.0,並且希望在 Web 窗體應用程式中使用數據源控制件進行數據綁定,則它們非常有用。

- [開始使用實體框架 4.0](../web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)。 展示如何使用**實體數據來源**控制項。
- [繼續實體框架](../web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)(示範如何使用**ObjectDataSource**控制件)。 包括關於併發處理的教程、關於 EF 性能的教程以及有關 EF 4.0 中新增功能的教程。

<a id="efrelateddata"></a>

### <a name="handling-related-data-in-entity-framework-lazy-loading-eager-loading-and-explicit-loading"></a>在實體框架中處理相關資料(延遲載入、熱切載入和顯式載入)

- [在 ASP.NETmVC 應用程式中使用實體框架讀取相關資料](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代碼優先,MVC 範例應用程式。 顯示的方法也適用於 Web 窗體模型綁定和資料庫優先工作流。
- [數據開發人員中心 - 載入相關實體](https://msdn.microsoft.com/data/jj574232)(MSDN)。 實體框架團隊有關載入相關數據的文件。

<a id="optimizingef"></a>

### <a name="optimizing-entity-framework-performance"></a>優化實體框架效能

- [ASP.NET應用程式的進階實體架構機制](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。 演示如何執行自己的 SQL 語句或調用自己的儲存過程、如何禁用更改檢測以及如何在保存更改時禁用驗證。
- [實體框架 5](https://msdn.microsoft.com/data/hh949853) (MSDN) 的性能注意事項。
- [性能注意事項(實體框架](https://msdn.microsoft.com/library/cc853327))(MSDN)。
- [在 ASP.NET Web 應用程式中使用實體框架最大化性能](../web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)。 適用於實體框架 4.0。
- 請參考此主題的圖形[的 ASP.NET 資料存取](#optimizingdataaccess)。

<a id="efconcurrency"></a>

### <a name="handling-concurrency-in-an-entity-framework-application"></a>在實體框架應用程式處理並發性

- [在 ASP.NET mVC 應用程式處理與實體框架的併發](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。 代碼優先,DbContext API,使用 MVC 範例應用程式。
- [數據開發人員中心 – 樂觀併發模式](https://msdn.microsoft.com/data/jj592904)(MSDN)。 實體框架團隊的併發文檔。
- [在 ASP.NET Web 應用程式處理與實體框架的併發](../web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)。 適用於實體框架 4.0。 資料庫優先,物件上下文 API,使用 Web 窗體範例應用程式。

<a id="efrepository"></a><a id="efbooks"></a>

### <a name="books-about-the-entity-framework"></a>有關實體框架的書籍

- [程式設計實體框架:裘莉](http://shop.oreilly.com/product/0636920022237.do)·萊曼和羅文·米勒的DbContext。
- [程式設計實體框架:裘莉](http://shop.oreilly.com/product/0636920022220.do)·萊曼和羅文·米勒首先編寫代碼。

這兩本書都是最新的最新推薦技術。 與互聯網上任何可用的內容相比,它們為實體框架提供了更全面但易於遵循的介紹。 另一本書,由裘莉·萊曼[程式設計實體框架](http://shop.oreilly.com/product/9780596807252.do),是更大和更全面的,但它是舊的,它涵蓋的許多技術不再是推薦的方式使用實體框架。 另請參閱[資料開發人員中心實體](https://msdn.microsoft.com/data/aa937716)框架團隊推薦的書籍清單 - MSDN 網站上的書籍。

<a id="otherefresources"></a>

### <a name="other-entity-framework-resources"></a>其他實體框架資源

- [實體框架 (ADO.NET) 團隊部落格](https://blogs.msdn.com/b/adonet/). 最新資訊和發佈新增強功能的最佳資源之一。 有關其他與 EF 相關的部落格,請參閱「[開始實體框架」](https://msdn.microsoft.com/data/ee712907)中的部落格卷。
- [MSDN雜誌](https://msdn.microsoft.com/magazine/default.aspx). 請參閱 **「數據點**」列,該列經常介紹與實體框架相關的主題。

<a id="wfdatabinding"></a>

## <a name="data-binding-in-aspnet-web-forms-applications"></a>ASP.NET Web 表單應用程式中的資料繫結

- [ASP.NET Web 窗體資料存取選項](https://msdn.microsoft.com/library/jj822927.aspx)(MSDN) 。<a id="wfmodelbinding"> </a>

<a id="wfmodelbinding"></a>

### <a name="using-web-forms-model-binding"></a>使用 Web 表單模型繫結

- [模型繫結與 Web 窗體](https://go.microsoft.com/fwlink/?LinkId=286117)。 使用 EF 代碼優先的教程系列。
- [Web 表單模型綁定第 1 部分:選擇數據](https://weblogs.asp.net/scottgu/archive/2011/09/06/web-forms-model-binding-part-1-selecting-data-asp-net-vnext-series.aspx)(斯科特·古斯裡博客)。 在這些較舊的部落格文章中,目前名為 ItemType 的屬性名為 ModelType,但除此之外,它們包含的資訊是有效的。
- [Web 表單模型綁定第 2 部分:篩選數據](https://weblogs.asp.net/scottgu/archive/2011/09/12/web-forms-model-binding-part-2-filtering-data-asp-net-vnext-series.aspx)(斯科特·古斯裡博客)。
- [Web 表單模型綁定第 3 部分:更新和驗證](https://weblogs.asp.net/scottgu/archive/2011/10/30/web-forms-model-binding-part-3-updating-and-validation-asp-net-4-5-series.aspx)(斯科特·古斯裡博客)。
- [ASP.NET 4.5 Web 窗體模型繫結](../web-forms/videos/aspnet-web-forms-vnext/aspnet-45-web-forms-model-binding.md)。 (視頻)。
- [模型繫結第 1 部分 - 選擇資料](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-1-selecting-data.md)(視頻)。
- [模型綁定第 2 部分 - 篩選](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-model-binding-part-2-filtering.md)(視頻)。
- [開始使用ASP.NET 4.5 Web 表單 - 顯示資料項目與詳細資訊](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。

<a id="wfdsc"></a>

### <a name="using-web-forms-data-source-controls"></a>使用 Web 表單資料來源控制項

- [數據源 Web 伺服器控制件](https://msdn.microsoft.com/library/ms247258.aspx)(MSDN)。
- [宣佈發佈實體框架 6 的動態數據提供程式和實體數據來源控制件](https://blogs.msdn.com/b/webdev/archive/2014/02/28/announcing-the-release-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)(Microsoft Web 開發部落格)。

<a id="wfdbc"></a>

### <a name="using-web-forms-data-bound-controls-and-data-binding-expressions"></a>使用 Web 表單資料繫結件和資料繫結式

- [模型繫結與 Web 窗體](https://go.microsoft.com/fwlink/?LinkId=286117)。 首先使用 EF 代碼的教程系列。
- [開始使用ASP.NET 4.5 Web 表單 - 顯示資料項目與詳細資訊](../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details.md)。
- [強類型數據控制](https://weblogs.asp.net/scottgu/archive/2011/09/02/strongly-typed-data-controls-asp-net-vnext-series.aspx)(斯科特·古斯裡博客)。
- [強類型數據控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)(視頻)。
- [ASP.NET 4.5 Web 窗體強類型數據控制](../web-forms/videos/aspnet-web-forms-vnext/aspnet-vnext-videos-strongly-typed-data-controls.md)(視頻)。
- [數據繫結 Web 伺服器控制件](https://msdn.microsoft.com/library/ms228214.aspx)(MSDN)。
- [數據繫式概述](https://msdn.microsoft.com/library/ms178366.aspx)(MSDN)。 本頁僅涵蓋**Eval**和**Bind**;它尚未更新,包括**專案和****連結項目**。

<a id="sqlserver"></a>

## <a name="working-with-sql-server-databases"></a>使用 SQL 伺服器資料庫

- [SQL 伺服器資料庫功能](https://msdn.microsoft.com/library/hh230827.aspx)(MSDN)。 有關各種 SQL Server 主題的一般介紹,請參閱 TOC 中此主題下的條目。
- [SQL 伺服器版本](https://msdn.microsoft.com/library/ms178359.aspx#sqlserver)(MSDN)。 可用 SQL Server 版本的摘要,並包含指向每個版本的詳細資訊的連結。
- 用於 ASP.NET Web 應用程式 (MSDN)[的 SQL 伺服器連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。
- [將 SQL 伺服器壓縮用於 ASP.NET Web 應用程式](https://msdn.microsoft.com/library/ms247257.aspx)(MSDN)。
- [微軟 SQL 伺服器:資料庫產品範例](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 示例冒險工程資料庫。
- [安裝範例資料庫](https://github.com/Microsoft/sql-server-samples/blob/master/samples/databases/adventure-works/README.md)。 除了此處顯示的方法外,您還可以將其中一個範例 .mdf 檔案下載\_到 Web 專案的 App Data 資料夾,將資料庫轉換為本地 DB,並創建 LocalDB 連接字串。 有關如何執行此操作的資訊,請參閱[如何:升級到本地資料庫](https://msdn.microsoft.com/library/hh873188.aspx)。

有關使用 SQL Server Express 和本地 DB 以及 SQL Server 和 SQL 資料庫之間的選擇,請參閱以下部分。

<a id="sslocaldb"></a>

### <a name="working-with-sql-server-express-localdb-databases"></a>使用 SQL 伺服器快速本地資料庫

- [SQL 伺服器快速 2012 本機資料庫](https://msdn.microsoft.com/library/hh510202(v=sql.110).aspx)(MSDN)。 本地 DB 的官方 MSDN 介紹。
- 用於 ASP.NET Web 應用程式 (MSDN)[的 SQL 伺服器連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。
- [如何:升級到本地資料庫](https://msdn.microsoft.com/library/hh873188.aspx)(MSDN)。 如何將 .mdf 檔從早期版本的 SQL Server Express 移至本地DB。 如果下載[SQL Server 2012 範例資料庫](https://go.microsoft.com/fwlink/?linkid=117483)之一,還必須完成此過程。
- [介紹本地資料庫,改進後的 SQL Express(SQL](https://go.microsoft.com/fwlink/?LinkId=234375)伺服器快速部落格)。 與 MSDN 中包含的背景相比,具有更多有關創建 LocalDB 的原因的背景。
- [本地資料庫:我的資料庫在哪裡?](https://go.microsoft.com/fwlink/?LinkId=234376) (SQL 伺服器快速博客)。 有關本地DB資料庫文件的創建位置的資訊。
- [將本地DB與完整IIS一起使用,第1部分:使用者配置檔](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-1-user-profile.aspx)(SQL伺服器快速博客)。 本地DB並非旨在與IIS配合使用。 這一系列博客文章解釋了問題和一些解決方法。

<a id="sse"></a>

### <a name="working-with-sql-server-express-databases"></a>使用 SQL 伺服器快速資料庫

- 用於 ASP.NET Web 應用程式 (MSDN)[的 SQL 伺服器連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。 如果將附加DBFileName連接字串設置與 SQL Server Express 一起使用,請參閱此頁面的使用者實例部分。
- [如何取得本地 SQL Server Express 2008(SQL Server Express](https://blogs.msdn.com/b/sqlexpress/archive/2010/02/23/how-to-take-ownership-of-your-local-sql-server-2008-express.aspx)部落格)的擁有權。 常見的問題是不能使用 SQL Server Express 資料庫,因為您不是 SQL Server Express 實體上的管理員。 默認情況下,只有安裝 SQL Server Express 的人員是管理員。 此部落格說明如果您是電腦上的管理員,如何使自己成為 SQL Server Express 管理員。
- [我的ASP.NET Web 應用程式是否可以在生產中使用 SQL Server Express 資料庫?](https://msdn.microsoft.com/library/jj653753.aspx#sql_express_in_production) (MSDN)。

<a id="ssdb"></a>

### <a name="working-with-windows-azure-sql-database"></a>使用 Windows Azure SQL 資料庫

- [將具有成員資格、OAuth 和 SQL 資料庫的安全ASP.NET MVC 應用部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)(Microsoft Azure 網站)。
- [SQL 資料庫](https://docs.microsoft.com/azure/sql-database/)(微軟 Azure 網站)。 入門教程和入門指南。
- [Windows Azure SQL 資料庫](https://msdn.microsoft.com/library/windowsazure/ee336279.aspx)(MSDN)。 MSDN 中 SQL 資料庫的目錄的頂級節點。
- [Windows Azure SQL 資料庫 TechNet 維琪文章索引](https://social.technet.microsoft.com/wiki/contents/articles/2267.windows-azure-sql-database-technet-wiki-articles-index-en-us.aspx)(微軟技術網網站)。
- [暫態容錯處理應用程式區](https://msdn.microsoft.com/library/hh680934(v=PandP.50).aspx)塊 。 一個框架,使您能夠處理由限制導致的瞬態網路故障和連接錯誤。 在 NuGet 套件中提供:[企業庫 5.0 - 暫態故障處理應用程式區](http://nuget.org/packages/EnterpriseLibrary.WindowsAzure.TransientFaultHandling)塊 。
- [開始使用 SQL 資料庫和實體框架](https://msdn.microsoft.com/data/jj556244)(MSDN)。
- [Windows Azure 培訓工具組](https://www.microsoft.com/download/details.aspx?id=8396)(微軟下載中心)。 包括用於 SQL 資料庫的動手實驗。
- [Windows Azure SQL 資料庫社區論壇](https://social.msdn.microsoft.com/Forums/ssdsgetstarted/threads)。
- [移動到 Windows Azure SQL 資料庫](https://msdn.microsoft.com/library/ff803375.aspx)(MSDN)。 Microsoft 模式和實踐團隊全面端到端方案的一章。 介紹了可能想要遷移的原因以及如何從 SQL Server 遷移到 SQL 資料庫。
- [將 SQL 伺服器資料庫遷移到 Windows Azure SQL 資料庫](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx)(MSDN)。
- [SQL 資料庫移轉精靈](http://sqlazuremw.codeplex.com/)。 用於將資料庫遷移到 SQL 資料庫和從 SQL 資料庫遷移到的開源工具。

<a id="ssdbchoosing"></a>

### <a name="choosing-between-sql-server-and-windows-azure-sql-database"></a>在 SQL 伺服器與 Windows Azure SQL 資料庫之間進行選擇

- [將 SQL 伺服器與 Windows Azure SQL 資料庫](https://social.technet.microsoft.com/wiki/contents/articles/996.compare-sql-server-with-windows-azure-sql-database-en-us.aspx)(微軟技術網站)進行比較。
- [數據移到 Windows Azure SQL 資料庫:工具和技術](https://msdn.microsoft.com/library/windowsazure/hh694043.aspx)(MSDN)。 包括將 SQL Server 與 SQL 資料庫進行比較的部分,並提供有關何時從 SQL Server 遷移到 SQL 資料庫的指導。
- [Windows Azure SQL 資料庫交付指南](https://social.technet.microsoft.com/wiki/contents/articles/3398.windows-azure-sql-database-delivery-guide-en-us.aspx)(微軟技術網網站)。
- [SQL 伺服器功能限制(Windows Azure SQL 資料庫](https://msdn.microsoft.com/library/windowsazure/ff394115.aspx))(MSDN)。
- [Windows Azure 表儲存和 Windows Azure SQL 資料庫 - 比較和對比](https://msdn.microsoft.com/library/jj553018.aspx)(MSDN)。 對於部署到 Windows Azure 的應用程式,Windows Azure 表存儲可能是 Windows Azure SQL 資料庫的替代方法。 本主題可説明您在這些備選方案之間進行決策。
- [Windows Azure SQL 資料庫](https://msdn.microsoft.com/library/windowsazure/ee336279)(MSDN)。
- [指導方針和限制 (Windows Azure SQL Database)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)

<a id="nosql"></a>

## <a name="working-with-nosql-database-management-systems"></a>使用 NoSQL 資料庫管理系統

- [Windows Azure 數據服務](https://www.windowsazure.com/develop/net/data/)(微軟 Azure 網站)。 請參閱[頁面的「表服務」功能指南](https://docs.microsoft.com/azure/)和**大數據**部分。
- [ASP.NET使用儲存表、佇列和Blob(Microsoft](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) Azure 網站)的多層應用程式。 使用 Windows Azure 儲存 NoSQL 表的可下載範例應用程式的端到端教程。

<a id="linq"></a>

## <a name="using-linq-queries-in-aspnet-applications"></a>在ASP.NET應用程式中使用 LINQ 查詢

- [ASP.NET資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx#linq)(MSDN)。 包括 LINQ 簡介。
- [LINQ培訓視頻](http://www.misfitgeek.com/windows-client-linq-training-videos-20/)(喬·斯塔格納的博客)。
- [ASP.NET論壇執行緒與動態LINQ資源的連結](https://forums.asp.net/p/1961037/5601994.aspx?Please+suggest+good+books+so+that+one+can+write+and+understand+dynamic+linq)。

<a id="dd"></a>

## <a name="using-dynamic-data-scaffolding"></a>使用動態資料基架

- [動態數據專案範本](https://msdn.microsoft.com/library/jj822927.aspx#dynamicdata)(MSDN)。 有關何時使用動態數據項目的指導。
- [ASP.NET動態資料](https://msdn.microsoft.com/library/ee845452.aspx)(MSDN)。

<a id="securing"></a>

## <a name="securing-data-access"></a>保護資料存取

- 保護ASP.NET (MSDN)[中的資料存取](https://msdn.microsoft.com/library/ms178375.aspx)。
- [安全注意事項(實體框架](https://msdn.microsoft.com/library/cc716760.aspx))(MSDN)。
- [如何:使用資料源控制項](https://msdn.microsoft.com/library/ms178372.aspx)(MSDN) 時保護連接字串。

<a id="optimizingdataaccess"></a>

## <a name="optimizing-data-access-performance"></a>優化資料存取效能

- [ASP.NET性能概述](https://msdn.microsoft.com/library/cc668225.aspx)(MSDN)。
- [ASP.NET緩存](https://msdn.microsoft.com/library/xsbfdd8c.aspx)(MSDN)。
- [提高ASP.NET性能](https://msdn.microsoft.com/library/ff647787)(MSDN)。 此頁面頂部有"已停用內容"警告,但大多數信息仍相關,並且沒有可比較的更新資源。
- [提高 SQL 伺服器性能](https://msdn.microsoft.com/library/ff647793)(MSDN)。 與上一個連結相同的註釋。

請參考此主題的設定的實體[框架效能](#optimizingef)。

<a id="deploying"></a>

## <a name="deploying-a-database"></a>部署資料庫

- [ASP.NET Web 部署 - 建議資源](aspnet-web-deployment-content-map.md)(MSDN)。

<a id="webservice"></a>

## <a name="accessing-data-through-a-web-service"></a>透過 Web 服務存取資料

- [通過 Web 服務](https://msdn.microsoft.com/library/ms178359.aspx#webservice)(MSDN) 訪問數據。 有關何時使用 Web API 與 WCF 的指導。
- [開始使用ASP.NET Web API](../web-api/index.md)。
- [WCF 資料服務](https://msdn.microsoft.com/data/bb931106)(MSDN)。

<a id="additional"></a>

## <a name="additional-resources"></a>其他資源

- [ASP.NET資料存取常見問題解答](https://msdn.microsoft.com/library/jj653753.aspx)(MSDN)。
- [ASP.NET Web 表單教學 - 資料](../web-forms/overview/data-access/index.md)。 這些教程大多比較舊;請確保首先閱讀[ASP.NET 資料存取選項](https://msdn.microsoft.com/library/ms178359.aspx)和[資料儲存選項(使用 Windows Azure 構建真實世界雲端應用),](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options.md)以免過多地進入不適合您的方案的資料存取方法。
- [ASP.NET MVC 內容映射](../mvc/overview/getting-started/recommended-resources-for-mvc.md)。
- [ASP.NET網頁教學 - 資料](../web-pages/overview/data/index.md)。
- [訪問視覺化工作室](https://msdn.microsoft.com/library/wzabh8c4.aspx)(MSDN) 中的數據。 提供與此內容映射類似的連結清單,但側重於可視化工作室,而不是ASP.NET。
