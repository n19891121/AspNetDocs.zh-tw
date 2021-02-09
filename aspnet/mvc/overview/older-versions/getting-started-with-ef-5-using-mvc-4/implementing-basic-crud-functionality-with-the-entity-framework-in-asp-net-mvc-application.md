---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行基本的 CRUD 功能 (2 之 10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f388aca4a0a6dc924417b3adc3ba5ef940e7104e
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985005"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>使用 ASP.NET MVC 應用程式中的 Entity Framework 來執行基本的 CRUD 功能 (2 之 10) 

由 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已建立 MVC 應用程式，該應用程式會使用 Entity Framework 和 SQL Server LocalDB 來儲存及顯示資料。 在本教學課程中，您將複習和自訂 CRUD (建立、讀取、更新、刪除) 程式碼，MVC 樣板會在控制器和 views 中自動為您建立。

> [!NOTE]
> 實作儲存機制模式，以在您的控制器及資料存取層之間建立抽象層是一種非常常見的做法。 為了簡化這些教學課程，您將不會在本系列稍後的教學課程中執行存放庫。

在本教學課程中，您將建立下列網頁：

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>建立詳細資料頁面

學生頁面的 scaffold 程式碼 `Index` `Enrollments` 會離開屬性，因為該屬性會保存集合。 在 `Details` 頁面中，您會將集合的內容顯示在 HTML 資料表中。

 在 *Controllers\StudentController.cs* 中，view 的動作方法會 `Details` 使用 `Find` 方法來取出單一 `Student` 實體。 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 金鑰值會以參數的形式傳遞至方法 `id` ，並來自 [索引] 頁面上 [ **詳細** 資料] 超連結中的路由資料。 

1. 開啟 *Views\Student\Details.cshtml*。 每個欄位都會使用 helper 來顯示 `DisplayFor` ，如下列範例所示： 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. 在欄位之後， `EnrollmentDate` 以及緊接在結尾 `fieldset` 標記之前，加入程式碼以顯示註冊清單，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    此程式碼會以迴圈逐一巡覽 `Enrollments` 導覽屬性中的實體。 針對屬性中的每個 `Enrollment` 實體，會顯示課程標題和等級。 課程標題會從 `Course` 實體的導覽屬性中儲存的實體中取出 `Course` `Enrollments` 。 當需要時，系統會自動從資料庫中取出所有資料。  (換句話說，您會在這裡使用消極式載入。 您未指定導覽屬性的 *積極式載入* `Courses` ，所以當您第一次嘗試存取該屬性時，系統會將查詢傳送至資料庫以取得資料。 您可以在本系列稍後的 [閱讀相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 教學課程中，閱讀更多有關消極式載入和積極式載入的資訊。 ) 
3. 選取 [ **學生** ] 索引標籤，然後按一下 [Alexander Carson] 的 [ **詳細資料** ] 連結，以執行頁面。 您會看到選取學生的課程及成績清單：

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>更新 [建立] 頁面

1. 在 *Controllers\StudentController.cs* 中， `HttpPost``Create` 以下列程式碼取代動作方法，以將 `try-catch` 區塊和 [Bind 屬性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) 新增至 scaffold 方法： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    這段程式碼會將 `Student` ASP.NET MVC 模型系結器建立的實體新增至 `Students` 實體集，然後將變更儲存至資料庫。  (*模型* 系結器指的是 ASP.NET MVC 功能，可讓您更輕鬆地使用表單所提交的資料;模型系結器會將張貼的表單值轉換為 CLR 類型，並將其傳遞至參數中的動作方法。 在此情況下，模型系結器 `Student` 會使用集合中的屬性值，為您具現化實體 `Form` 。 ) 

    `ValidateAntiForgeryToken`屬性有助於防止[跨網站偽造要求](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻擊。

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. 選取 [ **學生** ] 索引標籤，然後按一下 [ **建立新** 的]，以執行頁面。

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    某些資料驗證預設會運作。 輸入名稱和不正確日期，然後按一下 [ **建立** ] 以查看錯誤訊息。

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    下列反白顯示的程式碼顯示模型驗證檢查。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    將日期變更為有效的值（例如9/1/2005），然後按一下 [ **建立** ]，以查看新的學生是否出現在 [ **索引** ] 頁面中。

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>更新編輯後頁面

在 *Controllers\StudentController.cs* 中， `HttpGet` `Edit` 方法 (不含屬性的方法 `HttpPost`) 會使用 `Find` 方法來抓取選取的 `Student` 實體，如您在方法中所見 `Details` 。 您不需要變更這個方法。

不過，請 `HttpPost` `Edit` 以下列程式碼取代動作方法，以新增 `try-catch` 區塊和 [Bind 屬性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

此程式碼類似于您在方法中看到的內容 `HttpPost` `Create` 。 不過，此程式碼不會將模型系結器建立的實體新增至實體集，而是會在實體上設定旗標，指出已變更。 當呼叫 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 方法時， [修改過](https://msdn.microsoft.com/library/system.data.entitystate.aspx) 的旗標會使 Entity Framework 建立 SQL 語句，以更新資料庫資料列。 將會更新資料庫資料列的所有資料行，包括使用者未變更的資料行，而且會忽略並行衝突。  (您將在本系列稍後的教學課程中瞭解如何處理平行存取。 ) 

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>實體狀態和附加和 SaveChanges 方法

資料庫內容會追蹤實體在記憶體中是否與其在資料庫中相對應的資料列保持同步，並且此項資訊會決定當您呼叫 `SaveChanges` 方法時會發生什麼事情。 例如，當您將新的實體傳遞給 [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) 方法時，該實體的狀態會設為 `Added` 。 然後當您呼叫 [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) 方法時，資料庫內容會發出 SQL `INSERT` 命令。

實體可能會處於下列其中一種[狀態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)：

- `Added`. 實體尚未存在於資料庫中。 `SaveChanges`方法必須發出 `INSERT` 語句。
- `Unchanged`. `SaveChanges` 方法針對這個實體不需要進行任何動作。 當您從資料庫讀取一個實體時，實體便會以此狀態開始。
- `Modified`. 實體中一部分或全部的屬性值已經過修改。 `SaveChanges`方法必須發出 `UPDATE` 語句。
- `Deleted`. 實體已遭標示刪除。 `SaveChanges`方法必須發出 `DELETE` 語句。
- `Detached`. 實體未獲得資料庫內容追蹤。

在桌面應用程式中，狀態變更通常會自動進行設定。 在桌面類型的應用程式中，您會讀取實體，並對其屬性值進行變更。 這會使得其實體狀態自動變更為 `Modified`。 然後當您呼叫時 `SaveChanges` ，Entity Framework 會產生 SQL `UPDATE` 語句，只更新您變更的實際屬性。

Web apps 中斷連接的本質不允許此連續順序。 在轉譯頁面之後，會處置讀取實體的 [DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 。 呼叫 `HttpPost` `Edit` 動作方法時，會發出新的要求，而且您會有新的 [DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)實例，因此您必須手動設定實體狀態， `Modified.` 然後當您呼叫時 `SaveChanges` ，Entity Framework 會更新資料庫資料列的所有資料行，因為內容無法得知您變更的屬性。

如果您想要讓 SQL `Update` 語句只更新使用者實際變更的欄位，可以使用某些方式來儲存原始值 (例如隱藏欄位) ，以便在 `HttpPost` 呼叫方法時可以使用這些值 `Edit` 。 然後，您可以 `Student` 使用原始值建立實體、使用 `Attach` 該實體的原始版本來呼叫方法、將實體的值更新為新的值，然後呼叫 `SaveChanges.` 以取得詳細資訊，請參閱 MSDN 資料開發人員中心的 [實體狀態和 SaveChanges](https://msdn.microsoft.com/data/jj592676) 和 [本機資料](https://msdn.microsoft.com/data/jj592872) 。

*Views\Student\Edit.cshtml* 中的程式碼與您在 *Create. cshtml* 中看到的程式碼類似，且不需要任何變更。

選取 [ **學生** ] 索引標籤，然後按一下 [ **編輯** ] 超連結，以執行頁面。

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

變更一部分的資料，然後按一下 [儲存]。 您會在 [索引] 頁面中看到已變更的資料。

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>更新 [刪除] 頁面

在 *Controllers\StudentController.cs* 中，方法的範本程式碼 `HttpGet` `Delete` 會使用 `Find` 方法來抓取選取的 `Student` 實體，如您在和方法中所見 `Details` `Edit` 。 然而，若要在呼叫 `SaveChanges` 失敗時實作自訂錯誤訊息，您需要將一些功能新增至此方法及其對應的檢視。

如同您在更新及建立作業中所看到的，刪除作業需要兩個動作方法。 回應 GET 要求所呼叫的方法會顯示一個視圖，讓使用者有機會核准或取消刪除作業。 若使用者核准，則便會建立 POST 要求。 發生這種情況時， `HttpPost` `Delete` 會呼叫方法，然後該方法會實際執行刪除作業。

您會將 `try-catch` 區塊加入至 `HttpPost` `Delete` 方法，以處理更新資料庫時可能發生的任何錯誤。 如果發生錯誤，方法會 `HttpPost` `Delete` 呼叫 `HttpGet` `Delete` 方法，並將指出發生錯誤的參數傳遞給它。 `HttpGet Delete`方法接著會重新顯示確認頁面和錯誤訊息，讓使用者有機會取消或再試一次。

1. `HttpGet` `Delete` 以下列可管理錯誤報表的程式碼取代動作方法： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    此程式碼會接受 [選擇性](https://msdn.microsoft.com/library/dd264739.aspx) 的布林值參數，指出是否在儲存變更失敗之後呼叫它。 此參數是在 `false` `HttpGet` `Delete` 沒有先前失敗的情況下呼叫方法時。 當方法呼叫它來 `HttpPost` `Delete` 回應資料庫更新錯誤時，參數為，而且會將 `true` 錯誤訊息傳遞給視圖。
2. `HttpPost` `Delete` 以下列程式碼取代名為) 的動作方法 (，此程式 `DeleteConfirmed` 代碼會執行實際的刪除作業並攔截任何資料庫更新錯誤。

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     此程式碼會抓取選取的實體，然後呼叫 [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) 方法，將實體的狀態設定為 `Deleted` 。 當 `SaveChanges` 呼叫時， `DELETE` 會產生 SQL 命令。 您也將動作方法的名稱從 `DeleteConfirmed` 變更為 `Delete`。 名為方法的 scaffold 程式碼， `HttpPost` `Delete` `DeleteConfirmed` 讓 `HttpPost` 方法成為唯一的簽章。  ( CLR 要求多載方法必須有不同的方法參數。 ) 簽章是唯一的，您可以堅持使用 MVC 慣例，並針對 `HttpPost` 和 delete 方法使用相同的名稱 `HttpGet` 。

     如果在高容量應用程式中改善效能，您可以使用下列程式碼來取代呼叫和方法的程式程式碼，以避免不必要的 SQL 查詢取得資料列， `Find` `Remove` 如黃色醒目提示所示：

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     此程式碼會 `Student` 使用主鍵值來具現化實體，然後將實體狀態設定為 `Deleted` 。 這便是 Entity Framework 要刪除實體所需要的一切資訊。

     如上所述， `HttpGet` `Delete` 方法不會刪除資料。 執行刪除作業來回應 GET 要求 (或針對此情況，執行任何編輯作業、建立作業，或任何其他變更資料) 的作業都會產生安全性風險。 如需詳細資訊，請參閱 [ASP.NET MVC 提示 #46 —請勿使用刪除連結，因為它們會](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) 在 Stephen Walther 的 blog 上建立安全性漏洞。
3. 在 *Views\Student\Delete.cshtml* 中，于 `h2` 標題和標題之間加入錯誤訊息 `h3` ，如下列範例所示：

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     選取 [ **學生** ] 索引標籤，然後按一下 [ **刪除** ] 超連結，以執行頁面：

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. 按一下 **[刪除]** 。 顯示的 [索引] 頁面將不會包含遭刪除的學生。  (您會在本系列稍後的 [處理並行](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 存取教學課程中，看到錯誤處理常式代碼的範例。 ) 

## <a name="ensuring-that-database-connections-are-not-left-open"></a>確保資料庫連接不會保持開啟

若要確定資料庫連接是否已正確關閉，以及它們所保存的資源已釋出，您應該會看到內容實例已處置。 這就是為什麼 scaffold 程式碼會在 StudentController.cs 中的類別結尾提供[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法 `StudentController` ，如下列範例所示： 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

基類 `Controller` 已實作為 `IDisposable` 介面，因此此程式碼只會將覆寫新增至 `Dispose(bool)` 方法，以明確地處置內容實例。

## <a name="summary"></a>摘要

您現在有一組完整的頁面，可針對實體執行簡單的 CRUD 作業 `Student` 。 您使用 MVC helper 來產生資料欄位的 UI 元素。 如需 MVC 協助程式的詳細資訊，請參閱 [使用 HTML helper 轉譯表單](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (頁面是針對 mvc 3，但仍與 mvc 4) 相關。

在下一個教學課程中，您將藉由新增排序和分頁來擴充 [索引] 頁面的功能。

您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 
> [下一步](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
