---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 將 ASP.NET MVC 應用程式中的存放庫和工作單元模式 (9 的 10) 中執行 |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5bcdf32f1aa48e0d4950f59ff7841413f6990812
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99984708"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>將 ASP.NET MVC 應用程式中的存放庫和工作單元模式 (9 （共10個）中執行) 

由 [Tom Dykstra](https://github.com/tdykstra)


> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您使用了繼承來減少 `Student` 和實體類別中的多餘程式碼 `Instructor` 。 在本教學課程中，您會看到一些使用儲存機制和工作單位模式來進行 CRUD 作業的方式。 如先前的教學課程所示，您將變更程式碼使用已建立的頁面，而不是建立新頁面的方式。

## <a name="the-repository-and-unit-of-work-patterns"></a>存放庫和工作單元模式

存放庫和工作單元模式的目的是要在應用程式的資料存取層和商務邏輯層之間建立抽象層。 實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。

在本教學課程中，您將會為每個實體類型執行存放庫類別。 針對 `Student` 實體類型，您將建立存放庫介面和儲存機制類別。 當您在控制器中具現化存放庫時，您將會使用介面，讓控制器接受任何可執行存放庫介面之物件的參考。 當控制器在 web 伺服器下執行時，它會收到可搭配 Entity Framework 使用的存放庫。 當控制器在單元測試類別下執行時，它會接收使用儲存資料的儲存機制，您可以輕鬆地操作測試，例如記憶體中的集合。

稍後在教學課程中，您將針對 `Course` 控制器中的和實體類型使用多個存放庫和工作單元類別 `Department` `Course` 。 工作單位類別會建立由所有儲存機制所共用的單一資料庫內容類別，以協調多個存放庫的工作。 如果您想要能夠執行自動化單元測試，您可以使用與存放庫相同的方式來建立和使用這些類別的介面 `Student` 。 不過，為了讓教學課程保持簡單，您將建立並使用這些類別，而不需要介面。

下圖顯示將控制器和內容類別之間的關聯性概念化的一種方法，相較于根本不使用儲存機制或工作單位模式。

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

您不會在此教學課程系列中建立單元測試。 如需使用使用存放庫模式的 MVC 應用程式進行 TDD 的簡介，請參閱逐步解說：搭配使用 [TDD 與 ASP.NET MVC](https://msdn.microsoft.com/library/ff847525.aspx)。 如需有關存放庫模式的詳細資訊，請參閱下列資源：

- MSDN 上[的存放庫模式](https://msdn.microsoft.com/library/ff649690.aspx)。
- 使用 Entity Framework team blog 上[Entity Framework 4.0 的儲存機制和工作單位模式](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx)。
- [Agile Entity Framework 4](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) Julie Lerman 的 blog 系列文章。
- 在 Dan Wahlin 的 blog 上，[以一目了然的 HTML5/JQuery 應用程式建立帳戶](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx)。

> [!NOTE]
> 有許多方式可以執行存放庫和工作單元模式。 您可以使用具有或不含工作單位類別的儲存機制類別。 您可以為所有實體類型或每種類型各執行一個儲存機制。 如果您針對每個類型執行一個，則可以使用不同的類別、泛型基類和衍生類別，或抽象基類和衍生類別。 您可以在存放庫中包含商務邏輯，或將它限制為數據存取邏輯。 您也可以使用 [idbset 會](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 介面（而不是實體集的 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 類型），在資料庫內容類別中建立抽象層。 執行本教學課程中所示之抽象層的方法，是您可以考慮的選項之一，而不是所有案例和環境的建議。

## <a name="creating-the-student-repository-class"></a>建立 Student 存放庫類別

在 *DAL* 資料夾中，建立名為 *IStudentRepository.cs* 的類別檔案，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

此程式碼會宣告一組一般的 CRUD 方法，包括兩個讀取方法：一個會傳回所有實體，另一個則 `Student` 會 `Student` 依識別碼尋找單一實體。

在 *DAL* 資料夾中，建立名為 *StudentRepository.cs* file 的類別檔案。 以下列程式碼取代現有的程式碼，此程式碼會 `IStudentRepository` 執行介面：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

資料庫內容定義于類別變數中，而此函式需要呼叫的物件傳入內容的實例：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

您可以在存放庫中具現化新的內容，但如果您在一個控制器中使用多個存放庫，則每個都有個別的內容。 稍後您將在控制器中使用多個存放庫 `Course` ，您會看到工作單位類別如何確保所有存放庫都使用相同的內容。

存放庫會執行 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) ，並處置您稍早在控制器中看到的資料庫內容，而其 CRUD 方法會以您稍早所見的相同方式來呼叫資料庫內容。

## <a name="change-the-student-controller-to-use-the-repository"></a>變更學生控制器以使用儲存機制

在 *StudentController.cs* 中，以下列程式碼取代目前在類別中的程式碼。 所做的變更已醒目提示。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

控制器現在會針對實 `IStudentRepository` 介面而非 coNtext 類別的物件，宣告類別變數：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

預設 (無參數) 的函式會建立新的內容實例，而選擇性的函式可讓呼叫端傳入內容實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

 (如果您使用的是相依性 *插入* 或 di，就不需要預設的函式，因為 DI 軟體可確保一律會提供正確的存放庫物件。 ) 

在 CRUD 方法中，現在會呼叫存放庫而非內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Dispose`方法現在會處置存放庫，而非內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

執行網站並按一下 [ **學生** ] 索引標籤。

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

頁面的外觀和運作方式與您變更程式碼以使用儲存機制之前相同，其他的學生頁面也相同。 不過， `Index` 控制器的方法進行篩選和排序的方式有很大的差異。 此方法的原始版本包含下列程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

更新的 `Index` 方法包含下列程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

只有反白顯示的程式碼已變更。

在原始版本的程式碼中， `students` 輸入為 `IQueryable` 物件。 查詢不會傳送至資料庫，直到使用像這樣的方法將它轉換成集合為止 `ToList` ，除非索引視圖存取 student 模型，否則不會發生這種情況。 `Where`上述原始程式碼中的方法會成為 `WHERE` SQL 查詢中傳送至資料庫的子句。 也就是說，資料庫只會傳回選取的實體。 不過，由於變更 `context.Students` 為 `studentRepository.GetStudents()` ， `students` 這個語句之後的變數就是 `IEnumerable` 包含資料庫中所有學生的集合。 套用方法的最終結果 `Where` 是相同的，但現在工作是在 web 伺服器的記憶體中完成，而不是由資料庫完成。 針對傳回大量資料的查詢，這可能沒有效率。

> [!TIP]
> 
> **IQueryable 與 IEnumerable 的比較**
> 
> 如這裡所示，執行存放庫之後，即使您在 [ **搜尋** ] 方塊中輸入某個內容，傳送至 SQL Server 的查詢會傳回所有的學生資料列，因為它不包含您的搜尋條件：
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 此查詢會傳回所有的學生資料，因為存放庫執行查詢時，不會知道搜尋準則。 在此情況下，排序、套用搜尋準則，以及選取資料子集以進行分頁 (僅顯示3個數據列的程式) 會在稍後於 `ToPagedList` 集合上呼叫方法時于記憶體中完成 `IEnumerable` 。
> 
> 在您執行存放庫) 之前的舊版程式碼 (中，除非您在套用搜尋準則之後，才將查詢傳送至資料庫，而在 `ToPagedList` 物件上呼叫時 `IQueryable` 。
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> 在物件上呼叫 ToPagedList 時 `IQueryable` ，傳送至 SQL Server 的查詢會指定搜尋字串，因此只會傳回符合搜尋條件的資料列，而且不需要在記憶體中進行任何篩選。
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
>  (下列教學課程說明如何檢查傳送至 SQL Server 的查詢。 ) 

下一節將說明如何執行儲存機制方法，讓您指定此工作應該由資料庫完成。

您現在已在控制器與 Entity Framework 資料庫內容之間建立抽象層。 如果您要使用此應用程式執行自動化單元測試，您可以在執行的單元測試專案中建立替代的儲存機制類別 `IStudentRepository` *。* 這個 mock 存放庫類別可以操作記憶體中的集合，以測試控制器函式，而不是呼叫內容來讀取和寫入資料。

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>執行泛型存放庫和工作單位類別

為每個實體類型建立存放庫類別可能會導致大量多餘的程式碼，而且可能會導致部分更新。 例如，假設您必須將兩個不同的實體類型更新為相同交易的一部分。 如果每個都使用不同的資料庫內容實例，則可能會成功，而另一個實例可能會失敗。 將多餘的程式碼降至最低的其中一種方式是使用一般儲存機制，以及確保所有存放庫都使用相同的資料庫內容 (，進而協調所有更新) 是使用工作單位類別的方式。

在本教學課程的這一節中，您將建立 `GenericRepository` 類別和 `UnitOfWork` 類別，並在控制器中使用它們 `Course` 來存取 `Department` 和 `Course` 實體集。 如先前所述，若要讓教學課程的這個部分保持簡單，您不會建立這些類別的介面。 但是，如果您要使用它們來協助 TDD，您通常會使用與存放庫相同的方式來執行這些介面 `Student` 。

### <a name="create-a-generic-repository"></a>建立一般儲存機制

在 *DAL* 資料夾中，建立 *GenericRepository.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

系統會為資料庫內容和儲存機制具現化的實體集宣告類別變數：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

此函數會接受資料庫內容實例，並初始化實體集變數：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get`方法會使用 lambda 運算式來允許呼叫程式碼指定篩選準則和資料行來排序結果，而字串參數則可讓呼叫端提供以逗號分隔的導覽屬性清單，以便進行積極式載入：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

此程式碼 `Expression<Func<TEntity, bool>> filter` 表示呼叫端會根據類型提供 lambda 運算式 `TEntity` ，而此運算式會傳回布林值。 例如，如果為實體型別具現化存放庫 `Student` ，則呼叫方法中的程式碼可能會 `student => student.LastName == "Smith` &quot; 為 `filter` 參數指定。

此程式碼 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 也表示呼叫端會提供 lambda 運算式。 但是在此情況下，運算式的輸入是型別的 `IQueryable` 物件 `TEntity` 。 運算式會傳回該物件的排序版本 `IQueryable` 。 例如，如果為實體型別具現化存放庫 `Student` ，則呼叫方法中的程式碼可能會 `q => q.OrderBy(s => s.LastName)` 為 `orderBy` 參數指定。

方法中的 `Get` 程式碼會建立 `IQueryable` 物件，然後套用篩選運算式（如果有的話）：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

接著，它會在剖析以逗號分隔的清單之後，套用立即載入的運算式：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

最後，它會套用 `orderBy` 運算式（如果有的話），並傳回結果，否則會傳回未排序查詢的結果：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

當您呼叫 `Get` 方法時，您可以針對方法所傳回的集合進行篩選和排序， `IEnumerable` 而不是為這些函數提供參數。 但是排序和篩選工作接著會在 web 伺服器的記憶體中完成。 藉由使用這些參數，您可以確保工作是由資料庫而不是 web 伺服器來完成。 替代方式是建立特定實體類型的衍生類別，並新增特殊 `Get` 方法，例如 `GetStudentsInNameOrder` 或 `GetStudentsByName` 。 不過，在複雜的應用程式中，這可能會導致大量的這類衍生類別和特殊方法，這可能更適合維護。

`GetByID`、和方法中的 `Insert` 程式碼與 `Update` 您在非泛型存放庫中看到的程式碼類似。  (您未在簽章中提供積極的載入參數 `GetByID` ，因為您無法使用方法來進行積極式載入 `Find` 。 ) 

針對方法提供兩個多載 `Delete` ：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

其中一項可讓您只傳入要刪除之實體的識別碼，而其中一個會接受實體實例。 如您在 [處理並行](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 存取教學課程中所見，針對並行處理，您需要一個 `Delete` 方法，該方法會採用包含追蹤屬性之原始值的實體實例。

此一般存放庫將處理一般的 CRUD 需求。 當特定實體類型具有特殊需求（例如更複雜的篩選或排序）時，您可以建立具有該型別之其他方法的衍生類別。

## <a name="creating-the-unit-of-work-class"></a>建立工作單位類別

工作單位類別有一個用途：為了確保當您使用多個存放庫時，它們會共用單一資料庫內容。 如此一來，當工作單位完成時，您就可以 `SaveChanges` 在該內容實例上呼叫方法，並確保所有相關的變更都將會協調。 類別需要的所有方法都是 `Save` 方法和每個存放庫的屬性。 每個存放庫屬性都會傳回已使用與其他存放庫實例相同的資料庫內容實例來具現化的儲存機制實例。

在 *DAL* 資料夾中，建立名為 *UnitOfWork.cs* 的類別檔案，並以下列程式碼取代範本程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

程式碼會為資料庫內容和每個存放庫建立類別變數。 若為 `context` 變數，則會具現化新的內容：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

每個存放庫屬性都會檢查存放庫是否已存在。 如果沒有，則會具現化存放庫，並在內容實例中傳遞。 因此，所有存放庫都會共用相同的內容實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save`方法會 `SaveChanges` 在資料庫內容上呼叫。

就像任何在類別變數中具現化資料庫內容的類別一樣，該類別會實 `UnitOfWork` `IDisposable` 和處置內容。

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>變更課程式控制制器以使用 UnitOfWork 類別和儲存機制

以下列程式碼取代您目前在 *CourseController.cs* 中所擁有的程式碼：

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

這段程式碼會加入類別的類別變數 `UnitOfWork` 。  (如果您在這裡使用介面，則不會在此初始化變數;相反地，您會執行兩個函式的模式，就像您對存放庫所做的一樣 `Student` 。 ) 

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

在類別的其餘部分，對適當存放庫的參考會取代資料庫內容的所有參考，並使用 `UnitOfWork` 屬性來存取存放庫。 `Dispose`方法會處置 `UnitOfWork` 實例。

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

執行網站並按一下 [ **課程** ] 索引標籤。

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

頁面的外觀和運作方式與您的變更之前相同，其他課程頁面也相同。

## <a name="summary"></a>摘要

您現在已實作為存放庫和工作單元模式。 您已使用 lambda 運算式作為一般存放庫中的方法參數。 如需有關如何搭配物件使用這些運算式的詳細資訊 `IQueryable` ，請參閱 MSDN Library 中的 [IQueryable (T) 介面 (System. Linq) ](https://msdn.microsoft.com/library/bb351562.aspx) 。 在下一個教學課程中，您將瞭解如何處理一些 advanced 案例。

您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
