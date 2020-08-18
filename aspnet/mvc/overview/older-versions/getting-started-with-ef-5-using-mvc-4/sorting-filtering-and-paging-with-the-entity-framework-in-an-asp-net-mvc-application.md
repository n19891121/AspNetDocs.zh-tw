---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 進行排序、篩選和分頁 (3/10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 48938b378a741a0f1c351c2cb1d33b5140c6cf93
ms.sourcegitcommit: 8d34fb54e790cfba2d64097afc8276da5b22283e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85484398"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>使用 ASP.NET MVC 應用程式中的 Entity Framework 進行排序、篩選和分頁 (3/10) 

由 [Tom Dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從開頭開始進行教學課程系列，或 [下載此章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md) ，從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已針對實體的基本 CRUD 作業，執行一組網頁 `Student` 。 在本教學課程中，您會將排序、篩選和分頁功能新增至 **學生** 的 [索引] 頁面。 此外，還要建立將執行簡易群組的頁面。

下圖顯示當您完成時的頁面外觀。 資料行標題是使用者可以按一下以依據該資料行排序的連結。 重覆按一下資料行標題，可切換遞增和遞減排序次序。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>將資料行排序連結新增至 Students 的 [索引] 頁面

若要將排序新增至學生的 [索引] 頁面，您將變更 `Index` 控制器的方法， `Student` 並將程式碼加入至 `Student` 索引視圖。

### <a name="add-sorting-functionality-to-the-index-method"></a>將排序功能加入至 Index 方法

在 *Controllers\StudentController.cs*中，以 `Index` 下列程式碼取代方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此程式碼會從 URL 中的查詢字串接收 `sortOrder` 參數。 ASP.NET MVC 會提供查詢字串值，做為動作方法的參數。 該參數是 "Name" 或 "Date" 的字串，後面可選擇性地接著底線和字串 "desc" 來指定遞減順序。 預設排序順序為遞增。

第一次要求 [索引] 頁面時，沒有任何查詢字串。 學生會以遞增的順序顯示 `LastName` ，也就是由語句中的逐步執行案例所建立的預設值 `switch` 。 使用者按一下資料行標題超連結時，適當的 `sortOrder` 值將會在查詢字串值中提供。

`ViewBag`系統會使用這兩個變數，讓 view 可以使用適當的查詢字串值來設定資料行標題超連結：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

這些是三元陳述式。 第一個是指定如果 `sortOrder` 參數是 null 或空白，則 `ViewBag.NameSortParm` 應該設定為 "name \_ desc"; 否則，它應該設定為空字串。 這兩個陳述式讓檢視能夠設定資料行標題超連結，如下所示：

| 目前排序次序 | 姓氏超連結 | 日期超連結 |
| --- | --- | --- |
| 姓氏遞增 | descending | ascending |
| 姓氏遞減 | ascending | ascending |
| 日期遞增 | ascending | descending |
| 日期遞減 | ascending | ascending |

方法會使用 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 來指定要排序的資料行。 程式碼會在語句之前建立 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 變數 `switch` 、在語句中修改它， `switch` 並在 `ToList` 語句之後呼叫方法 `switch` 。 當您建立和修改 `IQueryable` 變數時，沒有查詢會傳送至資料庫。 在您 `IQueryable` 呼叫方法（例如）將物件轉換成集合之前，不會執行查詢 `ToList` 。 因此，此程式碼會產生一個查詢，而此查詢在語句之前都不會執行 `return View` 。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>將資料行標題超連結新增至學生索引視圖

在 *Views\Student\Index.cshtml*中，以 `<tr>` 反 `<th>` 白顯示的程式碼取代標題資料列的和元素：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

此程式碼會使用屬性中的資訊 `ViewBag` ，以適當的查詢字串值設定超連結。

執行頁面，然後按一下 [ **姓氏** ] 和 [ **註冊日期] 資料** 行標題，以確認排序可正常運作。

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

當您按一下 [ **姓氏** ] 標題之後，學生會以姓氏順序顯示。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>將搜尋方塊新增至學生的 [索引] 頁面

若要將篩選新增至 Students 的 [索引] 頁面，您要將文字方塊和提交按鈕新增至檢視，並在 `Index` 方法中進行對應的變更。 文字方塊可讓您輸入要在名字和姓氏欄位中搜尋的字串。

### <a name="add-filtering-functionality-to-the-index-method"></a>將篩選功能新增至 Index 方法

在 *Controllers\StudentController.cs*中，以 `Index` 下列程式碼取代方法 () 會反白顯示變更：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

您已將 `searchString` 參數新增至 `Index` 方法。 您也已將子句新增至 LINQ 語句 `where` ，這個子句只會選取其名字或姓氏包含搜尋字串的學生。 搜尋字串值是從您將加入至索引視圖的文字方塊中收到。只有在有要搜尋的值時，才會執行加入 [where](https://msdn.microsoft.com/library/bb535040.aspx) 子句的語句。

> [!NOTE]
> 在許多情況下，您可以在 Entity Framework 實體集上呼叫相同的方法，或是在記憶體中的集合上呼叫擴充方法。 結果通常是相同的，但在某些情況下可能會有所不同。 例如， `Contains` 當您將空字串傳遞給它時，方法的 .NET Framework 執行會傳回所有資料列，但是 SQL Server Compact 4.0 的 Entity Framework 提供者會針對空字串傳回零個數據列。 因此，範例中的程式碼 (將 `Where` 語句放在 `if` 語句內) 可確保您取得所有 SQL Server 版本的相同結果。 此外，此方法的 .NET Framework 實 `Contains` 依預設會執行區分大小寫的比較，但是 Entity Framework SQL Server 提供者預設會執行不區分大小寫的比較。 因此，呼叫 `ToUpper` 方法以明確區分大小寫，可確保當您稍後變更程式碼以使用存放庫時，不會變更結果，而不會傳回 `IEnumerable` 集合而不是 `IQueryable` 物件。 (當您在 `IEnumerable` 集合上呼叫 `Contains` 方法時，將取得 .NET Framework 實作；當您在 `IQueryable` 物件上呼叫它時，則會取得資料庫提供者實作。)

### <a name="add-a-search-box-to-the-student-index-view"></a>將搜尋方塊新增至學生的 [索引] 檢視

在 *Views\Student\Index.cshtml*中，于開頭標記之前加入醒目提示的程式碼，以便 `table` 建立標題、文字方塊和 **搜尋** 按鈕。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

執行頁面，輸入搜尋字串，然後按一下 [ **搜尋** ] 以確認篩選是否正常運作。

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

請注意，URL 未包含「a」搜尋字串，這表示如果您將此頁面加入書簽，當您使用書簽時，將不會取得篩選過的清單。 您將在稍後的教學課程中，變更 [ **搜尋** ] 按鈕，以使用篩選準則的查詢字串。

## <a name="add-paging-to-the-students-index-page"></a>將分頁新增至學生索引頁面

若要將分頁新增至學生的 [索引] 頁面，您必須先安裝 **PagedList Mvc** NuGet 套件。 然後，您會在方法中進行其他變更 `Index` ，並將分頁連結新增至 `Index` 視圖。 **PagedList** 是 ASP.NET Mvc 的許多良好分頁和排序封裝的其中一種，其用途僅限於範例，而不是其他選項的建議。 下圖顯示頁面連結。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>安裝 PagedList MVC NuGet 套件

NuGet **PagedList** 套件會自動安裝 **PagedList** 套件作為相依性。 **PagedList**封裝會安裝 `PagedList` 和集合的集合型別和擴充方法 `IQueryable` `IEnumerable` 。 擴充方法會在或以外的集合中建立單一資料頁面 `PagedList` `IQueryable` `IEnumerable` ，而 `PagedList` 集合會提供數個可協助分頁的屬性和方法。 **PagedList**會安裝分頁協助程式，以顯示分頁按鈕。

從 [ **工具** ] 功能表選取 [ **nuget 封裝管理員** ]，然後 **管理方案的 nuget 套件**。

在 [ **管理 NuGet 封裝** ] 對話方塊中，按一下左側的 [ **線上** ] 索引標籤，然後在搜尋方塊中輸入「分頁」。 當您看到 **PagedList** 的封裝時，請按一下 [ **安裝**]。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在 [ **選取專案** ] 方塊中，按一下 **[確定]**。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>將分頁功能新增至 Index 方法

在 *Controllers\StudentController.cs*中，加入 `using` `PagedList` 命名空間的語句：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

以下列程式碼取代 `Index` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

這段程式碼會將 `page` 參數、目前的排序次序參數和目前的篩選參數新增至方法簽章，如下所示：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

第一次顯示頁面，或是使用者尚未按一下分頁或排序連結時，所有參數都會是 null。 如果按一下分頁連結， `page` 變數會包含要顯示的頁碼。

`A ViewBag` 屬性提供目前排序次序的視圖，因為這必須包含在分頁連結中，才能讓排序次序在分頁時保持相同：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

另一個屬性，則會 `ViewBag.CurrentFilter` 提供具有目前篩選字串的視圖。 此值必須包含在分頁連結中，才能維護分頁期間的篩選設定，而且它必須在頁面重新顯示時還原為文字方塊。 如果搜尋字串在分頁期間變更，頁面必須重設為 1，因為新的篩選可能會導致顯示不同的資料。 在文字方塊中輸入值並按下 [提交] 按鈕時，會變更搜尋字串。 在該情況下， `searchString` 參數不是 null。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

在方法的結尾， `ToPagedList` 學生物件的擴充方法 `IQueryable` 會將學生查詢轉換成支援分頁的集合類型中的單一學生頁面。 然後將該單一頁面傳給視圖：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 方法會採用頁面數。 這兩個問號代表 [null 聯合運算子](https://msdn.microsoft.com/library/ms173224.aspx)。 Null 聯合運算子將針對可為 Null 的型別定義預設值；`(page ?? 1)` 運算式表示在它含有值時會傳回值 `page`，或在 `page` 為 null 時傳回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>將分頁連結新增至學生索引視圖

在 *Views\Student\Index.cshtml*中，以下列程式碼取代現有的程式碼：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

頁面頂端的 `@model` 陳述式指定檢視現在會取得 `PagedList` 物件，而不是 `List` 物件。

的 `using` 語句 `PagedList.Mvc` 可為分頁按鈕的 MVC helper 提供存取權。

程式碼會使用 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 的多載，以允許它指定 [FormMethod. Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

預設 [html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 會使用 POST 提交表單資料，這表示參數會在 HTTP 訊息內文中傳遞，而不是以 URL 形式傳遞至查詢字串。 當您指定 HTTP GET 時，表單資料會以 URL 中作為查詢字串傳遞，這可讓使用者為該 URL 加上書籤。 [使用 HTTP GET 的 W3C 指導方針](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定當動作不會產生更新時，您應該使用 GET。

文字方塊會使用目前的搜尋字串來初始化，因此當您按一下新的頁面時，可以看到目前的搜尋字串。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

資料行標頭連結會使用查詢字串，將目前的搜尋字串傳遞至控制器，讓使用者可以在篩選結果內排序：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

目前的頁面和總頁數隨即顯示。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

如果沒有可顯示的頁面，則會顯示「0的頁面0」。  (在這種情況下，頁碼大於頁面計數 `Model.PageNumber` ，因為是1，且 `Model.PageCount` 是0。 ) 

協助程式會顯示分頁按鈕 `PagedListPager` ：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager`Helper 提供許多您可以自訂的選項，包括 url 和樣式。 如需詳細資訊，請參閱 GitHub 網站上的 [TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。

執行頁面。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

以不同排序次序按一下分頁連結，以確定分頁運作正常。 然後輸入搜尋字串並再次嘗試分頁，以確認分頁的排序和篩選能正確運作。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>建立顯示學生統計資料的 [About （關於）] 頁面

對於 Contoso 大學網站的 About 頁面，您將顯示每個註冊日期已有多少學生註冊。 這需要對群組進行分組和簡單計算。 若要完成此工作，您需要執行下列作業：

- 針對您需要傳遞至檢視的資料，建立檢視模型類別。
- 修改 `About` 控制器中的方法 `Home` 。
- 修改 `About` 視圖。

### <a name="create-the-view-model"></a>建立視圖模型

建立 *viewmodel* 資料夾。 在該資料夾中，新增類別檔案 *EnrollmentDateGroup.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改 Home 控制器

在 *HomeController.cs*中，將下列 `using` 語句新增至檔案頂端：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

在類別的左大括弧後面緊接著，加入資料庫內容的類別變數：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

以下列程式碼取代 `About` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 陳述式會依註冊日期將學生實體組成群組、計算每個群組中的實體數目、將結果儲存在 `EnrollmentDateGroup` 檢視模型物件的集合中。

新增 `Dispose` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改 About 檢視

將 *Views\Home\About.cshtml* 檔案中的程式碼取代為下列程式碼：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

執行應用程式，然後按一下 [ **關於** ] 連結。 每個註冊日期的學生人數將會顯示在資料表中。

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>選擇性：將應用程式部署到 Windows Azure

到目前為止，您的應用程式在您的開發電腦上 IIS Express 于本機執行。 若要讓其他人可透過網際網路使用它，您必須將它部署至 web 主機服務提供者。 在本教學課程的這個選擇性區段中，您會將其部署至 Windows Azure 網站。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>使用 Code First 移轉部署資料庫

若要部署資料庫，您將會使用 Code First 移轉。 當您建立用來設定從 Visual Studio 部署之設定的發行設定檔時，您會選取標示為 [執行] 的核取方塊， ** (在應用程式啟動) 上執行 Code First 移轉 **。 這項設定會導致部署程式在目的地伺服器上自動設定應用程式 *Web.config* 檔，讓 Code First 使用 `MigrateDatabaseToLatestVersion` 初始化運算式類別。

Visual Studio 在部署程式期間，不會對資料庫執行任何動作。 當部署的應用程式在部署之後第一次存取資料庫時，Code First 會自動建立資料庫，或將資料庫架構更新為最新版本。 如果應用程式是執行遷移 `Seed` 方法，則在建立資料庫或更新架構之後，便會執行此方法。

您的遷移 `Seed` 方法會插入測試資料。 如果您要部署到生產環境，則必須變更 `Seed` 方法，使其只會插入您想要插入至生產資料庫的資料。 例如，在您目前的資料模型中，您可能想要在開發資料庫中擁有真實的課程，但虛構的學生。 您可以撰寫 `Seed` 方法以在開發期間載入，然後在部署至生產環境之前，先將虛構的學生加上批註。 或者，您可以撰寫一個 `Seed` 方法來僅載入課程，並使用應用程式的 UI，以手動方式在測試資料庫中輸入虛構的學生。

### <a name="get-a-windows-azure-account"></a>取得 Windows Azure 帳戶

您將需要 Windows Azure 帳戶。 如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Windows Azure 免費試用](https://azure.microsoft.com/free/dotnet/)。

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>在 Windows Azure 中建立網站和 SQL 資料庫

您的 Windows Azure 網站將在共用主控環境中執行，這表示它會在與其他 Windows Azure 用戶端共用的虛擬機器 (Vm) 上執行。 共用主控環境是一種在雲端中開始營運的低成本方法。 因為應用程式是在專用 VM 上執行，所以如果日後您的 Web 流量增加，可依需求對應用程式進行延展。 如果您需要更複雜的架構，您可以遷移至 Windows Azure 雲端服務。 雲端服務是執行於您可視本身需求來設定的專用 VM 上。

Windows Azure SQL Database 是以 SQL Server 技術為基礎的雲端式關係資料庫服務。 使用 SQL Server 的工具和應用程式也可以使用 SQL Database。

1. 在 [ [Windows Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下左邊索引標籤中的 [ **網站** ]，然後按一下 [ **新增**]。

    ![管理入口網站中的 [新增] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. 按一下 [ **自訂建立**]。

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **新網站-[自訂建立**嚮導] 隨即開啟。
3. 在嚮導的 [ **新增網站** ] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式的唯一 URL。 完整的 URL 將包含您在此處輸入的字串，加上您在文字方塊旁看到的尾碼。 圖例顯示「ConU」，但該 URL 可能會被採用，因此您必須選擇不同的 URL。

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. 在 [ **區域** ] 下拉式清單中，選擇接近您的區域。 這項設定會指定您的網站將在哪一個資料中心執行。
5. 在 [ **資料庫** ] 下拉式清單中，選擇 [ **建立免費的 20 MB SQL Database**]。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. 在 [ **DB 連接字串名稱**] 中，輸入 *SchoolCoNtext*。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 按一下指向方塊底部右邊的箭號。 Wizard 會前進到 [ **資料庫設定** ] 步驟。
8. 在 [ **名稱** ] 方塊中，輸入 *ContosoUniversityDB*。
9. 在 [ **伺服器** ] 方塊中，選取 [ **新增 SQL Database 伺服器**]。 或者，如果您先前已建立伺服器，就可以從下拉式清單中選取該伺服器。
10. 輸入系統管理員 **登入名稱** 和 **密碼**。 如果選取 [新增 SQL Database 伺服器]****，則不要在此處輸入現有的名稱和密碼，而是輸入新的名稱和密碼；您現在定義的名稱和密碼將供未來存取資料庫時使用。 如果您選取先前建立的伺服器，則會輸入該伺服器的認證。 在本教學課程中，您不會選取 [ ***Advanced*** ] 核取方塊。 ***Advanced***選項可讓您設定資料庫定[序](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。
11. 選擇您為網站選擇的相同 **區域** 。
12. 按一下方塊右下角的核取記號，表示您已完成。   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    下圖顯示使用現有的 SQL Server 和登入。   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    管理入口網站回到 [網站] 頁面，[ **狀態** ] 欄會顯示正在建立網站。 在一段時間之後 (通常不到一分鐘的) ，[ **狀態** ] 資料行會顯示已成功建立網站。 在左側的導覽列中，您帳戶中的網站數目會出現在 [ **網站** ] 圖示旁，而資料庫數目會出現在 [ **SQL 資料庫** ] 圖示旁。

## <a name="deploy-the-application-to-windows-azure"></a>將應用程式部署到 Windows Azure

1. 在 Visual Studio 的 [方案總管]**** 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]****。  
  
    ![專案內容功能表中的 [發行]](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. 在**發佈 Web** wizard 的 [**設定檔**] 索引標籤中，按一下 [匯**入**]。  
  
    ![匯入發行設定](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. 如果您先前未在 Visual Studio 中新增 Windows Azure 訂用帳戶，請執行下列步驟。 在這些步驟中，您會新增訂用帳戶，以便 **從 Windows Azure** 網站匯入下的下拉式清單會包含您的網站。

    a. 在 [匯 **入發行設定檔** ] 對話方塊中，按一下 [ **從 windows Azure**網站匯入]，然後按一下 [ **新增 windows azure 訂閱**]。

    ![新增 Windows Azure 訂用帳戶](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. 在 [匯 **入 Windows Azure 訂閱** ] 對話方塊中，按一下 [ **下載訂閱**檔案]。

    ![下載訂用帳戶檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 在瀏覽器視窗中，儲存 *.publishsettings* 檔案。

    ![下載 .publishsettings 檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 安全性- *.publishsettings* 檔案包含您的認證 (未編碼的) ，用來管理您的 Windows Azure 訂閱和服務。 這個檔案的安全性最佳作法是暫時儲存在來原始目錄外部 (例如，在 *Libraries\Documents* 資料夾) 中，然後在匯入完成後將它刪除。 取得檔案存取權的惡意使用者 `.publishsettings` 可以編輯、建立及刪除您的 Windows Azure 服務。

    d. 在 [匯 **入 Windows Azure 訂閱** ] 對話方塊中，按一下 **[流覽]** 並流覽至 *.publishsettings* 檔案。

    ![下載 sub](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. 按一下 [匯入]  。

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. 在 [匯 **入發行設定檔** ] 對話方塊中，選取 [ **從 Windows Azure 網站匯入**]，從下拉式清單中選取您的網站，然後按一下 **[確定]**。  
  
    ![匯入發行設定檔](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. 在 [ **連接** ] 索引標籤中，按一下 [ **驗證連接** ]，確認設定正確無誤。  
  
    ![驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 驗證連接之後，[ **驗證** 連線] 按鈕旁邊會顯示綠色核取記號。 按一下 [下一步]  。  
  
    ![已成功驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. 開啟 [ **SchoolCoNtext** ] 底下的 [**遠端連線字串**] 下拉式清單，然後選取您所建立之資料庫的連接字串。
8. 選取 [ **執行] Code First 移轉 (在應用程式啟動) 上執行 **。
9. 取消核取 [ **在執行時間使用此連接字串** **UserCoNtext (DefaultConnection) **，因為此應用程式不會使用成員資格資料庫。   
  
    ![[設定] 索引標籤](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. 按一下 [下一步]  。
11. 在 [ **預覽** ] 索引標籤中，按一下 [ **開始預覽**]。  
  
    ![[預覽] 索引標籤中的 [StartPreview] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    索引標籤會顯示要複製到伺服器的檔案清單。 發佈應用程式時不需要顯示預覽，但這是很有用的功能。 在此情況下，您不需要對所顯示的檔案清單進行任何動作。 下一次部署此應用程式時，只有已變更的檔案才會出現在此清單中。  
  
    ![StartPreview 檔輸出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. 按一下 [發佈] 。  
    Visual Studio 開始將檔案複製到 Windows Azure 伺服器的程式。
13. [輸出] **** 視窗會顯示已採取的部署動作，並報告部署作業已順利完成。  
  
    ![報告部署成功的輸出視窗](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 部署成功後，預設瀏覽器會自動開啟至已部署網站的 URL。  
    您建立的應用程式現在正在雲端中執行。 按一下 [學生] 索引標籤。  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

此時您的 *SchoolCoNtext* 資料庫已在 Windows Azure SQL Database 中建立，因為您選取了 [ **執行] Code First 移轉 (會在應用程式啟動) 上 **執行。 已部署網站中的 *Web.config* 檔已變更，因此 [>migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始化運算式會在您第一次程式碼讀取或寫入資料庫中的資料時執行， (當您選取 [ **學生** ] 索引標籤時，會發生這種情況) ：

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

部署程式也會建立新的連接字串， * (SchoolCoNtext \_ DatabasePublish*) ，以便 Code First 移轉用來更新資料庫架構和植入資料庫。

![Database_Publish 連接字串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection*連接字串適用于在本教學課程中未使用的成員資格資料庫 () 。 ContosoUniversity 資料庫的 *SchoolCoNtext* 連接字串。

您可以在 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*的電腦上找到 Web.config 檔案的已部署版本。您可以使用 FTP 來存取已部署的 *Web.config* 檔案本身。 如需相關指示，請參閱 [使用 Visual Studio：部署程式碼更新 ASP.NET Web 部署](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 遵循開頭為「若要使用 FTP 工具的指示，您需要三個專案： FTP URL、使用者名稱和密碼。」

> [!NOTE]
> Web 應用程式不會執行安全性，因此尋找 URL 的任何人都可以變更資料。 如需如何保護網站的相關指示，請參閱 [使用成員資格、OAuth 和 SQL Database 將安全的 ASP.NET MVC 應用程式部署到 Windows Azure 網站](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 您可以使用 Windows Azure 管理入口網站或 Visual Studio 中的 **伺服器總管** ，防止其他人使用該網站來停止網站。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First 初始化運算式

在 [部署] 區段中，您會看到使用的是 [>migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 初始化運算式。 Code First 也提供可供您使用的其他初始化運算式，包括 [>createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (預設) 、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 和 [DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways`初始化運算式有助於設定單元測試的條件。 您也可以撰寫自己的初始化運算式，如果您不想等到應用程式讀取或寫入資料庫，也可以明確地呼叫初始化運算式。 如需初始化運算式的完整說明，請參閱本書程式設計 Entity Framework 的第6章 [： Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan 莎莎。

## <a name="summary"></a>摘要

在本教學課程中，您已瞭解如何建立資料模型，以及如何執行基本的 CRUD、排序、篩選、分頁和群組功能。 在下一個教學課程中，您將會藉由展開資料模型來開始查看更多的主題。

您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md) 
> [下一步](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
