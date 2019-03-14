---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 中實作 Entity framework 的 CRUD 功能 |Microsoft Docs
description: 檢閱並自訂建立、 讀取、 更新、 刪除 (CRUD) 程式碼，在控制器和檢視中自動建立的 MVC scaffolding。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064075"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>教學課程：在 ASP.NET MVC 中實作 Entity framework 的 CRUD 功能

在 [先前的教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，建立 MVC 應用程式來儲存和使用 SQL Server LocalDB 與 Entity Framework (EF) 6 顯示資料。 在本教學課程中，您檢閱和自訂的建立、 讀取、 更新、 刪除 (CRUD) MVC scaffolding 自動為您建立控制器和檢視表中的程式碼。

> [!NOTE]
> 實作儲存機制模式，以在您的控制器及資料存取層之間建立抽象層是一種非常常見的做法。 若要簡單並聚焦於教導如何使用 EF 6 本身，請保留這些教學課程中，它們不使用存放庫。 如需如何實作存放庫資訊，請參閱[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)。

以下是您所建立之 web 網頁的範例：

![Student [詳細資料] 頁面的螢幕擷取畫面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![學生的螢幕擷取畫面中建立頁面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![螢幕擷取畫面至學生刪除頁面。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立詳細資料頁面
> * 更新 [建立] 頁面
> * 更新的 HttpPost Edit 方法
> * 更新 *Delete* 頁面
> * 關閉資料庫連線
> * 處理交易

## <a name="prerequisites"></a>必要條件

* [建立 Entity Framework 資料模型](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>建立詳細資料頁面

Scaffold 的程式碼，讓學生`Index`向左翻頁`Enrollments`屬性，因為該屬性的值集合。 在 [ `Details` ] 頁面上，您將會以 HTML 表格顯示集合的內容。

在  *Controllers\StudentController.cs*，動作方法`Details`檢視使用[尋找](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx)方法來擷取單一`Student`實體。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

索引鍵的值會傳遞給方法的`id`參數，來自*將資料路由傳送*中**詳細資料**索引 頁面上的超連結。

### <a name="tip-route-data"></a>提示：**路由資料**

路由資料是在路由表中指定的 URL 區段中找到的模型繫結的資料。 例如，指定預設路由`controller`， `action`，和`id`區段：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

在下列 URL 中，對應的預設路由`Instructor`作為`controller`，`Index`作為`action`並 1 做為`id`; 這些是路由資料值。

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` 查詢字串值。 如果您傳遞，也會運作模型繫結`id`作為查詢字串值：

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Url 藉由`ActionLink`Razor 檢視中的陳述式。 下列程式碼中，`id`參數符合預設路由，因此`id`會新增至路由資料。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

下列程式碼，`courseID`不符合預設路由中的參數，所以它會加入做為查詢字串。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>若要建立的詳細資料頁面

1. 開啟*Views\Student\Details.cshtml*。

   每個欄位會顯示使用`DisplayFor`協助程式，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. 在後`EnrollmentDate`欄位，然後立即在關閉前`</dl>`標記中加入反白顯示的程式碼，以顯示一份註冊，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    如果您將程式碼之後，錯誤程式碼縮排，請按**Ctrl**+**K**， **Ctrl**+**D**格式化它。

    此程式碼會以迴圈逐一巡覽 `Enrollments` 導覽屬性中的實體。 每個`Enrollment`實體在屬性中，它會顯示課程標題及成績。 課程標題會從`Course`中所儲存的實體`Course`導覽屬性`Enrollments`實體。 所有這些資料是從資料庫擷取自動在需要時。 換句話說，您使用消極式載入這裡。 您未指定*積極式載入*如`Courses`導覽屬性，因此在相同的查詢取得學生未擷取註冊。 相反地，第一次您嘗試存取`Enrollments`導覽屬性，新的查詢傳送至資料庫擷取資料。 您可以深入了解消極式載入和中的積極式載入[讀取相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)稍後在本系列教學課程。

3. 開啟 [詳細資料] 頁面來啟動程式 (**Ctrl**+**F5**)，並選取**學生**] 索引標籤，然後按一下 [ **的詳細資料** Alexander Carson 的連結。 (如果您按下**Ctrl**+**F5**雖然*Details.cshtml*檔案開啟，您會收到 HTTP 400 錯誤。 這是因為 Visual Studio 會嘗試執行詳細資料 頁面中，但它沒有達到從指定的學生，若要顯示的連結。 如果發生這種情況，移除 URL 中的 [Student/詳細資料] 並再試一次，或者，關閉瀏覽器，以滑鼠右鍵按一下專案，然後按一下**檢視** > **瀏覽器中的檢視**。)

    您會看到所選學生的課程及成績清單。

4. 關閉瀏覽器。

## <a name="update-the-create-page"></a>更新 [建立] 頁面

1. 在  *Controllers\StudentController.cs*，取代<xref:System.Web.Mvc.HttpPostAttribute>`Create`動作方法，以下列程式碼。 這個程式碼加入`try-catch`區塊，並移除`ID`從<xref:System.Web.Mvc.BindAttribute>scaffold 方法的屬性：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    這個程式碼加入`Student`建立 ASP.NET MVC 模型繫結至實體`Students`實體設定，然後將變更儲存到資料庫。 *模型繫結器*指的 ASP.NET MVC 功能可讓您更輕鬆地由表單送出的資料搭配使用它，模型繫結至 CLR 型別值轉換張貼表單，並將它們傳遞至動作方法參數中。 在此情況下，模型繫結具現化`Student`實體，讓您使用屬性值從`Form`集合。

    您移除`ID`從繫結屬性，因為`ID`是 SQL Server 將資料列插入時自動設定的主要金鑰值。 使用者的輸入不會設定`ID`值。

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgerysecurityxsrfcsrf-prevention-in-aspnet-mvc-and-web-pagesmd-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>安全性警告-`ValidateAntiForgeryToken`屬性可協助防止[跨網站偽造要求](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻擊。 它需要對應`Html.AntiForgeryToken()`在檢視中，您稍後就會看到的陳述式。

    `Bind`屬性是一種方式防止*over-posting*中建立的案例。 例如，假設`Student`實體包含`Secret`您不想要設定這個 web 網頁的屬性。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    即使您尚未`Secret`欄位在網頁上，駭客可能使用一種工具，例如[fiddler](http://fiddler2.com/home)，或是撰寫 JavaScript，來張貼`Secret`表單值。 不含<xref:System.Web.Mvc.BindAttribute>屬性限制模型繫結時，它會建立所使用的欄位`Student`執行個體<em>，</em>模型繫結器會揀選`Secret`表單值並使用它來建立`Student`實體執行個體。 則無論駭客在 `Secret` 表單欄位中指定了什麼值，該值都會更新到您的資料庫中。 下圖顯示了 fiddler 工具新增`Secret`已張貼的表單值的欄位 （其值為"OverPost"）。

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    "OverPost" 的值會成功新增到插入資料列的 `Secret` 屬性中，即使您沒有要讓網頁設定該屬性。

    建議您最好使用`Include`參數搭配`Bind`屬性設定為*列入允許清單*欄位。 它也可使用`Exclude`參數*封鎖清單*您想要排除的欄位。 原因`Include`是更安全的是，當您將新屬性加入實體時，新的欄位不會自動受到`Exclude`清單。

    您可以防止大量指派在編輯案例中的，請先從資料庫讀取實體，然後呼叫`TryUpdateModel`，並傳入明確允許的屬性清單。 這是這些教學課程所使用的方法。

    防止大量指派由許多開發人員偏好的替代方式是使用模型繫結的檢視模型，而不是實體類別。 意即僅在檢視模型中包含您想要更新的屬性。 MVC 模型繫結器完成後，將檢視模型屬性複製到 實體執行個體，選擇性地使用這類工具[AutoMapper](http://automapper.org/)。 使用 db。若要將其狀態設定為 Unchanged，然後設定 Property("PropertyName") 實體執行個體上的項目。IsModified 設為 true，會包含在檢視模型中每個實體屬性。 這個方法可同時運用在編輯及建立案例中。

    以外`Bind`屬性，`try-catch`區塊是唯一您對 scaffold 程式碼所做的變更。 若在儲存變更時捕捉到衍生自 <xref:System.Data.DataException> 的例外狀況，則會顯示一般錯誤訊息。 <xref:System.Data.DataException> 例外狀況有時候是因為某些外部因素造成的，而非程式設計上的錯誤，因此系統會建議使用者再試一次。 雖然在此範例中並未實作，但生產環境品質的應用程式應記錄例外狀況。 如需詳細資訊，請參閱[監視及遙測 (使用 Azure 建置現實世界的雲端應用程式)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)中的**深入解析記錄檔**一節。

    中的程式碼*Views\Student\Create.cshtml*類似於您所見的內容中*Details.cshtml*，不同之處在於`EditorFor`和`ValidationMessageFor`協助程式會用於每個欄位，而不是`DisplayFor`. 以下是相關的程式碼：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create.cshtml*也包含`@Html.AntiForgeryToken()`，這適用於`ValidateAntiForgeryToken`屬性中的控制站，以協助防止[跨網站偽造要求](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻擊。

    不需要變更在*Create.cshtml*。

2. 執行頁面，來啟動程式中，選取**學生** 索引標籤，然後按一下**建立新**。

3. 輸入名稱和無效的日期，然後按一下**建立**以查看錯誤訊息。

    這是您取得預設的伺服器端驗證。 在稍後的教學課程中，您會看到如何將產生的用戶端驗證的程式碼的屬性。 下列醒目提示的程式碼顯示中的模型驗證檢查**建立**方法。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. 將日期變更為有效的值，然後按一下 [建立] 來在 [索引] 頁面上查看新增的學生。

5. 關閉瀏覽器。

## <a name="update-httppost-edit-method"></a>更新 HttpPost Edit 方法

1. 取代<xref:System.Web.Mvc.HttpPostAttribute>`Edit`動作方法，以下列程式碼：

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > 在*Controllers\StudentController.cs*，則`HttpGet Edit`方法 (沒有`HttpPost`屬性) 會使用`Find`方法來擷取所選`Student`實體，當您在中所見`Details`方法。 您不需要變更這個方法。

   這些變更會實作安全性最佳作法以防止[（overposting)](#overpost)，產生 scaffolder`Bind`屬性，並新增至實體集的已修改的旗標的模型繫結器建立的實體。 程式碼不再建議使用因為`Bind`屬性中未列出的欄位中任何預先存在的資料會清空`Include`參數。 在未來，MVC 控制器 scaffolder 將更新，讓其不會產生`Bind`編輯方法的屬性。

   新的程式碼會讀取現有的實體，呼叫<xref:System.Web.Mvc.Controller.TryUpdateModel%2A>更新中已張貼的表單資料中的使用者輸入的欄位。 Entity Framework 的自動變更追蹤集合[EntityState.Modified](<xref:System.Data.EntityState.Modified>)實體上的旗標。 當[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)呼叫方法時，<xref:System.Data.EntityState.Modified>旗標會使 Entity Framework 建立 SQL 陳述式來更新資料庫資料列。 [並行存取衝突](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)會被忽略，並更新資料庫的資料列的所有資料行，包括使用者未變更。 (稍後的教學課程示範如何處理並行衝突，如果您只想要更新資料庫中的個別欄位，您可以設定為實體[EntityState.Unchanged](<xref:System.Data.EntityState.Unchanged>)並將個別欄位設定為[EntityState.Modified](<xref:System.Data.EntityState.Modified>)。)

   若要防止大量指派，您想要更新 [編輯] 頁面的欄位會列入允許清單中的`TryUpdateModel`參數。 雖然目前沒有額外保護的欄位，但列出您希望模型繫結器繫結的欄位可確保您於未來將欄位新增到資料模型中時，新增的欄位會自動獲得保護，直到您明確的在這裡新增它們為止。

   基於這些變更，方法簽章的 HttpPost Edit 方法等同於 HttpGet edit 方法;因此您已重新命名方法 EditPost。

   > [!TIP]
   >
   > **實體狀態的附加和 SaveChanges 方法**
   >
   > 資料庫內容會追蹤實體在記憶體中是否與其在資料庫中相對應的資料列保持同步，並且此項資訊會決定當您呼叫 `SaveChanges` 方法時會發生什麼事情。 例如，當您傳遞至新的實體[新增](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)方法時，該實體的狀態會設為`Added`。 當您呼叫[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法，將資料庫內容會發出 SQL`INSERT`命令。
   >
   > 實體可能處於下列其中一種[狀態](xref:System.Data.EntityState):
   >
   > - `Added`. 在資料庫中尚未存在的實體。 `SaveChanges`方法必須發出`INSERT`陳述式。
   > - `Unchanged`. `SaveChanges` 方法針對這個實體不需要進行任何動作。 當您從資料庫讀取一個實體時，實體便會以此狀態開始。
   > - `Modified`. 實體中一部分或全部的屬性值已經過修改。 `SaveChanges`方法必須發出`UPDATE`陳述式。
   > - `Deleted`. 實體已遭標示刪除。 `SaveChanges`方法必須發出`DELETE`陳述式。
   > - `Detached`. 實體未獲得資料庫內容追蹤。
   >
   > 在桌面應用程式中，狀態變更通常會自動進行設定。 中的桌面應用程式類型，您會讀取一個實體，並變更其部分屬性值。 這會使得其實體狀態自動變更為 `Modified`。 當您呼叫`SaveChanges`，Entity Framework 會產生 SQL`UPDATE`陳述式可更新只有您所變更的實際的屬性。
   >
   > 中斷連接的 web 應用程式的本質不允許此連續順序。 [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)讀取實體頁面轉譯之後處置。 當`HttpPost``Edit`呼叫動作方法提出新要求時，您有的新執行個體[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)，因此您必須手動將實體狀態設定為`Modified.`然後當您呼叫`SaveChanges`，Entity Framework 會更新資料庫資料列的所有資料行，因為內容無從得知您變更的屬性。
   >
   > 如果您想要將 SQL`Update`陳述式來更新使用者實際變更的欄位，使其可用時，您可以在某些方面 （例如隱藏的欄位） 中儲存原始的值`HttpPost``Edit`呼叫方法。 然後您可以建立`Student`實體使用原始值，也就是呼叫`Attach`方法使用原始版本的實體，實體的值更新為新的值，然後再呼叫`SaveChanges.`如需詳細資訊，請參閱[實體狀態和 SaveChanges](/ef/ef6/saving/change-tracking/entity-state)並[本機資料](/ef/ef6/querying/local-data)。

   中的 HTML 和 Razor 程式碼*Views\Student\Edit.cshtml*類似於您所見的內容中*Create.cshtml*，並不不需要任何變更。

2. 執行頁面，來啟動程式中，選取**學生** 索引標籤，然後按一下**編輯**超連結。

3. 變更一部分的資料，然後按一下 [儲存]。 您會看到 [索引] 頁面中變更的資料。

4. 關閉瀏覽器。

## <a name="update-the-delete-page"></a>更新 *Delete* 頁面

在  *Controllers\StudentController.cs*，範本程式碼<xref:System.Web.Mvc.HttpGetAttribute>`Delete`方法會使用`Find`方法來擷取所選`Student`實體，當您在中所見`Details`和`Edit`方法。 然而，若要在呼叫 `SaveChanges` 失敗時實作自訂錯誤訊息，您需要將一些功能新增至此方法及其對應的檢視。

如同您在更新及建立作業中所看到的，刪除作業需要兩個動作方法。 呼叫以回應 GET 要求的方法會顯示檢視，給予使用者機會核准或取消刪除作業。 若使用者核准，則便會建立 POST 要求。 當發生這種情況`HttpPost``Delete`呼叫方法，然後該方法會實際執行刪除作業。

您會新增`try-catch`封鎖<xref:System.Web.Mvc.HttpPostAttribute>`Delete`方法來處理資料庫更新時可能會發生任何錯誤。 發生錯誤時， <xref:System.Web.Mvc.HttpPostAttribute> `Delete`方法呼叫<xref:System.Web.Mvc.HttpGetAttribute>`Delete`方法，將表示發生錯誤的參數傳遞給它。 <xref:System.Web.Mvc.HttpGetAttribute> `Delete`方法接著會重新顯示確認頁面及錯誤訊息，讓使用者有機會取消或再試一次。

1. 取代<xref:System.Web.Mvc.HttpGetAttribute>`Delete`動作方法，以下列程式碼，用來管理錯誤報告：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    此程式碼會接受[選擇性參數](https://msdn.microsoft.com/library/dd264739.aspx)，指出是否要將變更儲存在失敗後呼叫該方法。 這個參數是`false`時`HttpGet``Delete`而上一次的失敗不會呼叫方法。 當它由呼叫`HttpPost``Delete`方法以回應資料庫更新錯誤，參數是`true`和錯誤訊息傳遞至檢視。

2. 取代<xref:System.Web.Mvc.HttpPostAttribute>`Delete`動作方法 (名為`DeleteConfirmed`) 為下列程式碼，這會執行實際的刪除作業和攔截的任何資料庫更新錯誤。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    此程式碼會擷取選取的實體，然後呼叫[移除](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)方法，以將實體的狀態設定為`Deleted`。 當`SaveChanges`呼叫時，SQL`DELETE`命令會產生。 您也將動作方法的名稱從 `DeleteConfirmed` 變更為 `Delete`。 名為的 scaffold 程式碼`HttpPost``Delete`方法`DeleteConfirmed`給`HttpPost`方法唯一的簽章。 (CLR 要求多載方法必須要有不同的方法參數。)既然簽章是唯一的您可以繼續使用 MVC 慣例，並使用相同的名稱`HttpPost`和`HttpGet`delete 方法。

    改善效能的大量應用程式中做為優先考量，如果您無法避免不必要的 SQL 查詢來取代呼叫的程式碼行中擷取資料列`Find`和`Remove`為下列程式碼的方法：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    此程式碼會具現化`Student`使用只有主索引鍵值的實體，然後將實體狀態設定為`Deleted`。 這便是 Entity Framework 要刪除實體所需要的一切資訊。

    如所述， `HttpGet` `Delete`方法不會刪除資料。 執行刪除作業，以回應 GET 要求 （或就此而言，執行任何的編輯作業，建立作業或變更資料的任何其他作業） 會產生安全性風險。 如需詳細資訊，請參閱 < [ASP.NET MVC 秘訣 #46 — 不用刪除連結，因為它們會造成安全性漏洞](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)Stephen walther 所撰寫的部落格上。

3. 在  *Views\Student\Delete.cshtml*，新增一則錯誤訊息之間`h2`標題和`h3`標題之下，如下列範例所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. 執行頁面，來啟動程式中，選取**學生** 索引標籤，然後按一下**刪除**超連結。

5. 選擇**刪除**頁面上所顯示**確定您想要刪除此項目嗎？**。

    [索引] 頁面會顯示沒有遭刪除的學生。 (您會看到的錯誤處理中的作用中的程式碼範例[並行教學課程](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)。)

## <a name="close-database-connections"></a>關閉資料庫連線

關閉資料庫連接，並釋出資源，它們會儘速保存，請使用它完成時處置內容執行個體。 也就是為什麼包含 scaffold 的程式碼提供[處置](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法的結尾`StudentController`類別*StudentController.cs*，如下列範例所示：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

基底`Controller`已經類別會實作`IDisposable`介面，這個程式碼直接加入覆寫，以便`Dispose(bool)`明確處置內容執行個體的方法。

## <a name="handle-transactions"></a>處理交易

根據預設，Entity Framework 隱含性的實作了交易。 在案例中，您對多個資料列或資料表的變更，然後呼叫`SaveChanges`，Entity Framework 會自動可確保，所有變更的成功或全部失敗。 若有些變更已先完成，之後卻發生錯誤，則這些變更都會自動進行復原。 其中您需要更多控制的案例&mdash;比方說，如果您想要包含在交易中，Entity Framework 之外完成的作業&mdash;請參閱[使用交易](/ef/ef6/saving/transactions)。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您現在有一組完整的頁面，執行簡單的 CRUD 作業，如`Student`實體。 您可以用於 MVC 協助程式產生的資料欄位 UI 元素。 如需 MVC 協助程式的詳細資訊，請參閱[轉譯表單使用 HTML 協助程式](/previous-versions/aspnet/dd410596(v=vs.98))（發行項是為 MVC 3 但仍與 MVC 5）。

其他的 EF 6 資源連結可在[ASP.NET 資料存取-建議資源](../../../../whitepapers/aspnet-data-access-content-map.md)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立詳細資料頁面
> * 更新 [建立] 頁面
> * 更新的 HttpPost Edit 方法
> * 更新 [刪除] 頁面
> * 關閉資料庫連線
> * 處理的交易

請前往下一篇文章，以了解如何新增排序、 篩選和分頁至專案。
> [!div class="nextstepaction"]
> [排序、篩選與分頁](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
