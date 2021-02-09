---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 為 ASP.NET MVC 應用程式建立更複雜的資料模型 (4 的 10) |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 來建立 ASP.NET MVC 4 應用程式 .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 84e1218d29dd4d4afcf2b876c027b0579f012954
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985486"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>為 ASP.NET MVC 應用程式建立更複雜的資料模型， (4 的 10) 

由 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請 [下載已完成的章節](building-the-ef5-mvc4-chapter-downloads.md) ，並嘗試重現您的問題。 您通常可以藉由比較程式碼與已完成的程式碼，找到問題的解決方案。 針對一些常見的錯誤和解決方法，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在先前的教學課程中，您已使用由三個實體組成的簡單資料模型。 在本教學課程中，您將新增更多實體和關聯性，並透過指定格式、驗證和資料庫對應規則來自訂資料模型。 您會看到兩種自訂資料模型的方式：將屬性加入至實體類別，以及將程式碼加入至資料庫內容類別。

當您完成時，實體類別會構成如下列圖例中所顯示的完整資料模型：

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>使用屬性自訂資料模型

在本節中，您會了解到如何使用指定格式、驗證和資料庫對應規則的屬性來自訂資料模型。 然後，在下列幾節中，您將會藉 `School` 由將屬性加入至您已建立的類別，並為模型中其餘的實體類型建立新的類別，來建立完整的資料模型。

### <a name="the-datatype-attribute"></a>DataType 屬性

針對學生的註冊日期，所有網頁目前都會同時顯示時間和日期，即使您針對此欄位只需要日期而已。 使用資料註解屬性，您可以透過僅對一個程式碼進行變更，來修正每個顯示資料的檢視上的顯示格式。 為了查看如何進行此操作的範例，您將會新增一個屬性至 `Student` 類別中的 `EnrollmentDate` 屬性。

在 *Models\Student.cs* 中，加入 `using` 命名空間的語句， `System.ComponentModel.DataAnnotations` 並將 `DataType` 和 `DisplayFormat` 屬性新增至 `EnrollmentDate` 屬性，如下列範例所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性是用來指定比資料庫內建類型更明確的資料類型。 在此案例中，我們只想要追蹤日期，而非日期和時間。 [DataType 列舉](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)可提供許多資料類型，例如 *Date、Time、PhoneNumber、Currency、EmailAddress* 等等。 `DataType` 屬性也可讓應用程式自動提供類型的特定功能。 例如，您 `mailto:` 可以建立[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)的連結，而且可以為 datatype 提供日期選擇器。支援[HTML5](http://html5.org/)的瀏覽器[日期](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性會發出 html 5 瀏覽器可理解的 html 5 [資料](http://ejohn.org/blog/html-5-data-attributes/) (發音的 *資料虛線*) 屬性。 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性不提供任何驗證。

`DataType.Date` 未指定顯示日期的格式。 根據預設，資料欄位會根據伺服器之 [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)的預設格式顯示。

`DisplayFormat` 屬性用來明確指定日期格式：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

此 `ApplyFormatInEditMode` 設定會指定當值顯示在文字方塊中以供編輯時，也應該套用指定的格式。  (您可能不想要針對某些欄位（例如貨幣值），您可能不想要在文字方塊中編輯貨幣符號。 ) 

您可以單獨使用 [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 屬性，但通常最好也使用 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 屬性。 `DataType`屬性會傳達資料的 *語法*，而不是在螢幕上呈現資料的方式，並提供您無法取得的下列優點 `DisplayFormat` ：

- 瀏覽器可以啟用 HTML5 功能 (例如，顯示行事曆控制項、地區設定適當的貨幣符號、電子郵件連結等 ) 。
- 根據預設，瀏覽器會根據您的 [地區](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)設定，使用正確的格式來轉譯資料。
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性可以讓 MVC 選擇正確的欄位範本，在[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)時將資料轉譯 (如果本身使用字串範本) 的話。 如需詳細資訊，請參閱 Brad Wilson 的 [ASP.NET MVC 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。  (雖然是針對 MVC 2 所撰寫，但本文仍適用于 ASP.NET MVC 的最新版本。 ) 

如果您使用 `DataType` 具有日期欄位的屬性，則必須同時指定屬性， `DisplayFormat` 以確保欄位在 Chrome 瀏覽器中正確呈現。 如需詳細資訊，請參閱 [這個 StackOverflow 執行緒](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。

再次執行學生索引頁面，並注意註冊日期不會再顯示時間。 使用模型的任何視圖都同樣適用 `Student` 。

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

您也可以使用屬性指定資料驗證規則和訊息。 假設您想要確保使用者不會在名稱中輸入超過 50 個字元。 若要加入這項限制，請將 [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) 屬性新增至 `LastName` 和 `FirstMidName` 屬性，如下列範例所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性不會防止使用者輸入空白字元作為名稱。 您可以使用 [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 屬性將限制套用至輸入。 例如，下列程式碼要求第一個字元是大寫，而其餘字元則為字母順序：

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)屬性提供與[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性類似的功能，但不提供用戶端驗證。

執行應用程式，然後按一下 [ **學生** ] 索引標籤。您會收到下列錯誤：

*在建立資料庫之後，支援 ' SchoolCoNtext ' 內容的模型已變更。請考慮使用 Code First 移轉來更新資料庫 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)) 。*

資料庫模型已變更資料庫架構所需的變更，Entity Framework 偵測到這種情況。 您將會使用遷移來更新架構，而不會遺失您使用 UI 新增至資料庫的任何資料。 如果您變更了方法所建立的資料 `Seed` ，由於您在方法中使用的 [>addorupdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 方法，將會變更回其原始狀態 `Seed` 。  ([>addorupdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) 相當於來自資料庫術語的 "upsert" 作業。 ) 

請在套件管理員主控台 (PMC) 中輸入下列命令：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

此 `add-migration MaxLengthOnNames` 命令會建立名為 *&lt; timeStamp &gt; \_ MaxLengthOnNames.cs* 的檔案。 這個檔案包含的程式碼會更新資料庫，以符合目前的資料模型。 Entity Framework 會使用遷移檔案名前面加上的時間戳記來排序遷移。 在您建立多個遷移之後，如果您卸載資料庫，或使用遷移來部署專案，則所有的遷移都會依照建立的順序套用。

執行 [ **建立** ] 頁面，然後輸入超過50個字元的名稱。 當您超過50個字元時，用戶端驗證就會立即顯示錯誤訊息。

![用戶端 val 錯誤](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Column 屬性

您也可以使用屬性控制您的類別和屬性對應到資料庫的方式。 假設您已針對名字欄位使用 `FirstMidName` 作為名稱，因為欄位中可能也會包含中間名。 但您想要將資料庫資料行命名為 `FirstName`，因為撰寫臨機操作查詢資料庫的使用者比較習慣該名稱。 若要進行此對應，您可以使用 `Column` 屬性。

`Column` 屬性指定當建立資料庫時，`Student` 資料表中對應到 `FirstMidName` 屬性的資料行會命名為 `FirstName`。 換句話說，當您的程式碼參照 `Student.FirstMidName` 時，資料便會來自 `Student` 資料表中的 `FirstName` 資料行或在其中更新。 如果您未指定資料行名稱，則會提供與屬性名稱相同的名稱。

將 [ComponentModel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) 的 using 語句和資料行名稱屬性加入至 `FirstMidName` 屬性，如下列醒目提示的程式碼所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

加入資料 [行屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 會變更支援 SchoolCoNtext 的模型，因此它不會符合資料庫。 在 PMC 中輸入下列命令，以建立另一個遷移：

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

在 **伺服器總管** (**資料庫總管** 如果您使用 Express for Web) ，請按兩下 *Student* 資料表。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

下圖顯示在您套用前兩個遷移之前的原始資料行名稱。 除了從變更為的資料行名稱 `FirstMidName` `FirstName` ，兩個名稱資料行的長度已變更 `MAX` 為50個字元。

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

您也可以使用 [流暢的 API](https://msdn.microsoft.com/data/jj591617)進行資料庫對應變更，您稍後會在本教學課程中看到。

> [!NOTE]
> 如果您嘗試在完成所有這些實體類別的建立之前進行編譯，您可能會收到編譯器錯誤。

## <a name="create-the-instructor-entity"></a>建立 Instructor 實體

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

建立 *Models\Instructor.cs*，以下列程式碼取代範本程式碼：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

請注意，當中有幾個屬性跟 `Student` 和 `Instructor` 實體中的一樣。 在本系列稍後的「 [執行繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) 」教學課程中，您將會使用繼承來重構以消除這項冗余。

### <a name="the-required-and-display-attributes"></a>必要和顯示內容

屬性（attribute）上的屬性 `LastName` （attribute）會指定其為必要欄位，此文字方塊的標題應為「姓氏」 (而不是「姓氏」，而不是「姓氏」（沒有空間) ），而且值不能超過50個字元。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[StringLength 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)會設定資料庫中的最大長度，並為 ASP.NET MVC 提供用戶端和伺服器端驗證。 您也可以在此屬性中指定最小字串長度，但最小值不會對資料庫結構描述造成任何影響。 數值型別（例如 DateTime、int、double 和 float）不需要 [必要的屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) 。 無法將 null 值指派給實值型別，因此其本質上是必要的。 您可以移除 [必要的屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) ，並將它取代為屬性的最小長度參數 `StringLength` ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

您可以將多個屬性放在同一行，如此一來，您也可以撰寫講師類別，如下所示：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName 計算屬性

`FullName` 為一個計算屬性，會傳回藉由串連兩個其他屬性而建立的值。 因此，它只有一個 `get` 存取子，而且在 `FullName` 資料庫中不會產生任何資料行。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>課程和 OfficeAssignment 導覽屬性

`Courses` 和 `OfficeAssignment` 屬性為導覽屬性。 如先前所述，它們通常定義為 [虛擬](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) ，以便利用稱為消極式 [載入](https://msdn.microsoft.com/magazine/hh205756.aspx)的 Entity Framework 功能。 此外，如果導覽屬性可以保存多個實體，其型別必須實作為[ICollection &lt; T &gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)介面。  (例如[IList &lt; t &gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)有資格，但不符合[IEnumerable &lt; &gt; t](https://msdn.microsoft.com/library/9eekhta0.aspx) ，因為 `IEnumerable<T>` 不會執行[Add](https://msdn.microsoft.com/library/63ywd54z.aspx)。

講師可以教授任何數量的課程，所以 `Courses` 會定義為實體的集合 `Course` 。 我們的商務規則陳述講師最多隻能有一個辦公室，因此 `OfficeAssignment` 定義為單一 `OfficeAssignment` 實體 (這可能是因為 `null` 沒有任何辦公室指派) 。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>建立 OfficeAssignment 實體

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

使用下列程式碼建立 *Models\OfficeAssignment.cs* ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

建立專案，以儲存您的變更，並確認您尚未進行任何編譯器可以攔截的複製和貼上錯誤。

### <a name="the-key-attribute"></a>索引鍵屬性

和實體之間有一對零或一關聯性 `Instructor` `OfficeAssignment` 。 辦公室指派只存在於指派給的講師，因此其主要金鑰也是實體的外鍵 `Instructor` 。 但 Entity Framework 無法自動辨識 `InstructorID` 為此實體的主要金鑰，因為其名稱不符合 `ID` 或 *classname* `ID` 命名慣例。 因此，必須使用 `Key` 屬性將其識別為 PK：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

`Key`如果實體有自己的主鍵，但您想要將屬性命名為與或不同，您也可以使用屬性 `classnameID` `ID` 。 根據預設，EF 會將金鑰視為非資料庫產生，因為資料行是用於識別關聯性。

### <a name="the-foreignkey-attribute"></a>ForeignKey 屬性

當兩個實體之間有一對零或一關聯性或一對一關聯性時 (例如 `OfficeAssignment` 和 `Instructor`) 之間，EF 無法解決關聯性的哪一端是主體，而哪一端是相依的。 一對一關聯性在每個類別中都有一個參考導覽屬性，而另一個類別。 [ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以套用至相依類別以建立關聯性。 如果您省略 [ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，當您嘗試建立遷移時，會收到下列錯誤：

無法判斷 ' ContosoUniversity. OfficeAssignment ' 和 ' ContosoUniversity ' 類型之間關聯的主體端點。 您必須使用關聯性流暢的 API 或資料注釋，明確地設定此關聯的主要端點。

稍後在教學課程中，我們將示範如何使用流暢的 API 來設定此關聯性。

### <a name="the-instructor-navigation-property"></a>講師導覽屬性

此 `Instructor` 實體有一個可為 null 的 `OfficeAssignment` 導覽屬性 (，因為講師可能沒有) 的 office 指派，且該 `OfficeAssignment` 實體具有不可為 null 的 `Instructor` 導覽屬性 (因為沒有講師的 office 指派不存在--不可 `InstructorID` 為 null 的) 。 當 `Instructor` 實體有相關的 `OfficeAssignment` 實體時，每個實體都會在其導覽屬性中有另一個實體的參考。

您可以將 `[Required]` 屬性放在講師導覽屬性上，以指定必須有相關的講師，但您不需要這麼做，因為 InstructorID 外鍵 (也是此資料表的索引鍵) 不可為 null。

## <a name="modify-the-course-entity"></a>修改 Course 實體

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在 *Models\Course.cs* 中，將您先前新增的程式碼取代為下列程式碼：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

課程實體具有指向相關實體的外鍵屬性 `DepartmentID` `Department` ，而且它具有 `Department` 導覽屬性。 當您針對相關實體具有一個導覽屬性時，Entity Framework 便不需要您為資料模型新增一個外部索引鍵屬性。 EF 會在需要時自動在資料庫中建立外鍵。 但在資料模型中擁有外部索引鍵，可讓更新變得更為簡單和有效率。 例如，當您提取要編輯的課程實體時，如果您未載入該實體，則該 `Department` 實體為 null，因此當您更新課程實體時，您必須先提取該 `Department` 實體。 當外鍵屬性 `DepartmentID` 包含在資料模型中時，您不需要在 `Department` 更新之前提取實體。

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated 屬性

屬性上具有[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)參數的[DatabaseGenerated 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) `CourseID` 會指定主鍵值是由使用者提供，而不是由資料庫所產生。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

根據預設，Entity Framework 會假設主鍵值是由資料庫產生。 這是您在大多數案例下所希望的情況。 不過，對於 `Course` 實體，您將會使用使用者指定的課程編號，例如一個部門的1000系列、另一個部門的2000系列等等。

### <a name="foreign-key-and-navigation-properties"></a>外鍵和導覽屬性

實體中的外鍵屬性和導覽屬性 `Course` 反映了下列關聯性：

- 課程會指派給一個部門，因此基於上述理由，會有一個 `DepartmentID` 外部索引鍵和一個 `Department` 導覽屬性。 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- 由於課程可由任何數量的學生進行註冊，因此 `Enrollments` 導覽屬性為一個集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- 課程可由多個講師進行教授，因此 `Instructors` 導覽屬性為一個集合： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>建立部門實體

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

使用下列程式碼建立 *Models\Department.cs* ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column 屬性

稍早，您已使用資料 [行屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) 來變更資料行名稱對應。 在實體的程式碼中 `Department` ， `Column` 屬性是用來變更 SQL 資料類型對應，以便使用資料庫中的 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) 型別來定義資料行：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

通常不需要資料行對應，因為 Entity Framework 通常會根據您為屬性定義的 CLR 類型，選擇適當的 SQL Server 資料類型。 CLR `decimal` 類型會對應到 SQL Server 的 `decimal` 類型。 但是在此情況下，您知道資料行將會保留貨幣金額，而 [money](https://msdn.microsoft.com/library/ms179882.aspx) 資料類型更適合該資料類型。

### <a name="foreign-key-and-navigation-properties"></a>外鍵和導覽屬性

外部索引鍵及導覽屬性反映了下列關聯性：

- 部門可以有或沒有一位系統管理員，而系統管理員一律為講師。 因此， `InstructorID` 屬性會以外鍵的形式包含在 `Instructor` 實體中，並在類型指定之後加入問號， `int` 以將屬性標示為可為 null。導覽屬性會命名 `Administrator` 但保存 `Instructor` 實體： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- 某部門可能有許多課程，所以有一個 `Courses` 導覽屬性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > 根據慣例，Entity Framework 會為不可為 Null 的外部索引鍵和多對多關聯性啟用串聯刪除。 這可能會導致迴圈串聯刪除規則，這會在您的初始化運算式程式碼執行時造成例外狀況。 例如，如果您未將屬性定義 `Department.InstructorID` 為可為 null，當初始化運算式執行時，就會收到下列例外狀況訊息：「參考關聯性會導致不允許的迴圈參考。」 如果商務規則所需 `InstructorID` 的屬性為不可為 null，您就必須使用下列流暢的 API 來停用關聯性的串聯刪除： 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>修改 Student 實體

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

在 *Models\Student.cs* 中，將您先前新增的程式碼取代為下列程式碼。 所做的變更已醒目提示。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>註冊實體

 在 *Models\Enrollment.cs* 中，以下列程式碼取代您稍早新增的程式碼

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>外鍵和導覽屬性

外部索引鍵屬性及導覽屬性反映了下列關聯性：

- 註冊記錄乃針對單一課程，因此當中包含了一個 `CourseID` 外部索引鍵屬性及一個 `Course` 導覽屬性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- 註冊記錄乃針對單一學生，因此當中包含了一個 `StudentID` 外部索引鍵屬性及一個 `Student` 導覽屬性： 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>Many-to-Many Relationships

和實體之間有多對多關聯性，而實體函式則是 `Student` `Course` `Enrollment` *包含* 資料庫中承載的多對多聯結資料表。 這表示 `Enrollment` 此資料表包含聯結資料表外鍵以外的其他資料 (在此案例中，主鍵和 `Grade` 屬性) 。

下列圖例展示了在實體圖表中這些關聯性的樣子。  (此圖表是使用 [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)所產生;建立圖表不是教學課程的一部分，而是在這裡做為圖例使用 ) 

![學生-Course_many 至 many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

每個關聯線的一端都有1個，另一個星號 (\*) ，表示一對多關聯性。

如果 `Enrollment` 資料表不包含等級資訊，則只需要包含兩個外鍵 `CourseID` 和 `StudentID` 。 在這種情況下，它會對應至多對多的聯結資料表， *而不需要* 承載 (或資料庫中的 *單純聯結資料表*) ，您完全不需要為其建立模型類別。 `Instructor`和 `Course` 實體具有這種類型的多對多關聯性，而且您可以看到它們之間沒有實體類別：

![講師-Course_many 對 many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

但是，資料庫中必須有聯結資料表，如下列資料庫關係圖所示：

![講師-Course_many 對 many_relationship_tables](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework 會自動建立 `CourseInstructor` 資料表，而您可以藉由讀取和更新 `Instructor.Courses` 和導覽屬性，間接地讀取和更新資料表 `Course.Instructors` 。

## <a name="entity-diagram-showing-relationships"></a>顯示關聯性的實體圖表

下列圖例顯示了 Entity Framework Power Tools 為完成的 School 模型建立的圖表。

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

除了多對多關聯性線條 (\* 至 \*) 和一對多關聯性線 (1 到 \*) ，您可以在這裡看到一到零或一關聯性線條 (1 到 0 ..1) 介於 `Instructor` 和 `OfficeAssignment` 實體之間，以及零或一對多關聯性線條 (0 ..1 \* 之間) 到講師與部門實體之間。

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>藉由將程式碼加入資料庫內容來自訂資料模型

接下來，您會將新的實體新增至 `SchoolContext` 類別，並使用流暢的 [API](https://msdn.microsoft.com/data/jj591617) 呼叫來自訂一些對應。  (API 是「流暢的」，因為通常會將一系列的方法呼叫一起串連成單一語句，以供使用。 ) 

在本教學課程中，您只會將流暢的 API 用於無法使用屬性進行的資料庫對應。 然而，您也可以使用 Fluent API 指定大部分透過屬性可完成的格式、驗證及對應規則。 某些屬性 (例如 `MinimumLength`) 無法使用 Fluent API 來套用。 如先前所述， `MinimumLength` 不會變更架構，它只會套用用戶端和伺服器端驗證規則

某些開發人員偏好單獨使用 Fluent API，使其實體類別保持「整潔」。 若想要的話，您也可以混合使用屬性和 Fluent API，並且有一些自訂項目只能使用 Fluent API 完成。但一般來說，建議的做法是在這兩種方法中選擇其中一項，然後盡可能的一致使用該方法。

若要將新的實體加入至資料模型，並執行您未使用屬性執行的資料庫對應，請將 *DAL\SchoolCoNtext.cs* 中的程式碼取代為下列程式碼：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的新語句會設定多對多聯結資料表：

- 針對和實體之間的多對多關聯性 `Instructor` `Course` ，此程式碼會指定聯結資料表的資料表和資料行名稱。 Code First 可以為您設定多對多關聯性，而不需要此程式碼，但是如果您未呼叫它，就會取得預設名稱，例如資料 `InstructorInstructorID` `InstructorID` 行。

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

下列程式碼提供一個範例，說明如何使用流暢的 API （而非屬性）來指定和實體之間的關聯性 `Instructor` `OfficeAssignment` ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

如需「流暢的 API」語句在幕後執行的相關資訊，請參閱 [流暢的 api](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog 文章。

## <a name="seed-the-database-with-test-data"></a>使用測試資料植入資料庫

以下列程式碼取代 *Migrations\Configuration.cs* 檔中的程式碼，以提供您所建立之新實體的種子資料。

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

如您在第一個教學課程中所見，大部分的程式碼只會更新或建立新的實體物件，並視需要將範例資料載入屬性以進行測試。 不過，請注意， `Course` 與實體具有多對多關聯性的實體 `Instructor` 會如何處理：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

當您建立 `Course` 物件時，您會 `Instructors` 使用程式碼將導覽屬性初始化為空集合 `Instructors = new List<Instructor>()` 。 這可讓您使用方法來新增與 `Instructor` 此相關的實體 `Course` `Instructors.Add` 。 如果您未建立空的清單，將無法新增這些關聯性，因為 `Instructors` 屬性會是 null，且沒有 `Add` 方法。 您也可以將清單初始化新增至函式。

## <a name="add-a-migration-and-update-the-database"></a>新增遷移和更新資料庫

從 PMC 中，輸入 `add-migration` 下列命令：

`PM> add-Migration Chap4`

如果您嘗試在此時更新資料庫，您將會收到下列錯誤：

*ALTER TABLE 語句與外鍵條件約束「FK dbo」衝突 \_ 。當然是 \_ dbo。部門 \_ DepartmentID」。衝突發生在資料庫 "ContosoUniversity" 中，資料表 "dbo。部門 "，資料行 ' DepartmentID '。*

編輯 &lt; *時間戳記 &gt; \_ Chap4.cs* 檔，並進行下列程式碼變更 (您將加入 SQL 語句並修改 `AddColumn` 語句) ：

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

 (當您新增新行時，請務必將它標記為批註或刪除現有的 `AddColumn` 行，否則當您輸入命令時，將會收到錯誤 `update-database` 。 ) 

有時候，當您使用現有的資料來執行遷移時，您需要將存根資料插入資料庫，以滿足外鍵條件約束，而這就是您現在要做的事。 產生的程式碼會在資料表中加入不可為 null 的 `DepartmentID` 外鍵 `Course` 。 `Course`當程式碼執行時，如果資料表中已經有資料列，此作業 `AddColumn` 將會失敗，因為 SQL Server 不知道要在不可以是 null 的資料行中放置什麼值。 因此，您已變更程式碼，為新的資料行提供預設值，而且您已建立名為 "Temp" 的存根部門作為預設部門。 如此一 `Course` 來，當此程式碼執行時，如果有現有的資料列，這些資料列就會與「Temp」系所產生關聯。

當 `Seed` 方法執行時，它會在資料表中插入資料列， `Department` 並將現有資料 `Course` 列與這些新資料列產生關聯 `Department` 。 如果您在 UI 中尚未新增任何課程，則您不再需要「Temp」部門或資料行的預設值 `Course.DepartmentID` 。 若要允許某人使用應用程式來新增課程的可能性，您也需要更新 `Seed` 方法程式碼，以確保所有 `Course` 資料列都不只 (舊版的方法所插入的 `Seed` `DepartmentID` 資料列，在您從資料行移除預設值並刪除「暫存」部門之前，) 具有有效值。

完成 &lt; *時間戳記 &gt; \_ Chap4.cs* 檔的編輯之後，請 `update-database` 在 PMC 中輸入命令以執行遷移。

> [!NOTE]
> 您可以在遷移資料並進行架構變更時，收到其他錯誤。 如果您收到無法解決的遷移錯誤，您可以變更 *Web.config* 檔案中的連接字串，或刪除資料庫。 最簡單的方法是在 *Web.config* 檔案中重新命名資料庫。 例如，將資料庫名稱變更為 CU \_ 測試，如下列所示：
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> 有了新的資料庫，就不會有要遷移的資料，而且 `update-database` 命令更可能會在沒有錯誤的情況下完成。 如需有關如何刪除資料庫的指示，請參閱 [如何從 Visual Studio 2012 卸載資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。

如同您先前所做的一樣，在 **伺服器總管** 中開啟資料庫，然後展開 [ **資料表]** 節點，以查看所有資料表都已建立。  (如果您仍 **伺服器總管** 從較早的時間開啟，請按一下 [重新整理 **] 按鈕。** ) 

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

您未建立資料表的模型類別 `CourseInstructor` 。 如前文所述，這是與實體之間的多對多關聯性的聯結資料表 `Instructor` `Course` 。

在資料表上按一下滑鼠右鍵 `CourseInstructor` ，然後選取 [ **顯示資料表資料** ]，確認它有 `Instructor` 您加入至導覽屬性之實體的結果 `Course.Instructors` 。

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>摘要

您現在已有了更複雜的資料模型和對應的資料庫。 在下列教學課程中，您將深入瞭解存取相關資料的不同方式。

您可以在 [ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一個](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 
> [下一步](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
