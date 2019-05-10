---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 教學課程：建立更複雜的資料模型的 ASP.NET MVC 應用程式
author: tdykstra
description: 在本教學課程中，您將新增更多的實體和關聯性，並將指定格式、 驗證和資料庫對應規則來自訂資料模型。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5c27f6fe07856db2b2961abc8fa797343d361d97
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65120941"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a><span data-ttu-id="20adf-103">教學課程：建立更複雜的資料模型的 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="20adf-103">Tutorial: Create a more complex data model for an ASP.NET MVC app</span></span>

<span data-ttu-id="20adf-104">在上一個教學課程中您用過三個實體所組成的簡單資料模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-104">In the previous tutorials you worked with a simple data model that was composed of three entities.</span></span> <span data-ttu-id="20adf-105">您在本教學課程中新增更多的實體和關聯性，而您指定格式、 驗證和資料庫對應規則來自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-105">In this tutorial you add more entities and relationships and you customize the data model by specifying formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="20adf-106">本文將說明兩種方式可以自訂資料模型： 藉由將屬性加入至實體類別和程式碼加入至資料庫內容類別。</span><span class="sxs-lookup"><span data-stu-id="20adf-106">This article shows two ways to customize the data model: by adding attributes to entity classes and by adding code to the database context class.</span></span>

<span data-ttu-id="20adf-107">當您完成時，實體類別會構成如下列圖例中所顯示的完整資料模型：</span><span class="sxs-lookup"><span data-stu-id="20adf-107">When you're finished, the entity classes will make up the completed data model that's shown in the following illustration:</span></span>

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="20adf-109">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="20adf-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20adf-110">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="20adf-110">Customize the data model</span></span>
> * <span data-ttu-id="20adf-111">更新 Student 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-111">Update Student entity</span></span>
> * <span data-ttu-id="20adf-112">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-112">Create Instructor entity</span></span>
> * <span data-ttu-id="20adf-113">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-113">Create OfficeAssignment entity</span></span>
> * <span data-ttu-id="20adf-114">修改 Course 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-114">Modify the Course entity</span></span>
> * <span data-ttu-id="20adf-115">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-115">Create the Department entity</span></span>
> * <span data-ttu-id="20adf-116">修改 Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-116">Modify the Enrollment entity</span></span>
> * <span data-ttu-id="20adf-117">將程式碼加入至資料庫的內容</span><span class="sxs-lookup"><span data-stu-id="20adf-117">Add code to database context</span></span>
> * <span data-ttu-id="20adf-118">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-118">Seed database with test data</span></span>
> * <span data-ttu-id="20adf-119">新增移轉</span><span class="sxs-lookup"><span data-stu-id="20adf-119">Add a migration</span></span>
> * <span data-ttu-id="20adf-120">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-120">Update the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20adf-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="20adf-121">Prerequisites</span></span>

* [<span data-ttu-id="20adf-122">第一個移轉和部署程式碼</span><span class="sxs-lookup"><span data-stu-id="20adf-122">Code First migrations and deployment</span></span>](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a><span data-ttu-id="20adf-123">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="20adf-123">Customize the data model</span></span>

<span data-ttu-id="20adf-124">在本節中，您會了解到如何使用指定格式、驗證和資料庫對應規則的屬性來自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-124">In this section you'll see how to customize the data model by using attributes that specify formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="20adf-125">然後在下列各節的數個您要建立完整`School`加上的資料模型屬性類別已建立並建立新的類別，針對模型中剩餘的實體類型。</span><span class="sxs-lookup"><span data-stu-id="20adf-125">Then in several of the following sections you'll create the complete `School` data model by adding attributes to the classes you already created and creating new classes for the remaining entity types in the model.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="20adf-126">DataType 屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-126">The DataType Attribute</span></span>

<span data-ttu-id="20adf-127">針對學生的註冊日期，所有網頁目前都會同時顯示時間和日期，即使您針對此欄位只需要日期而已。</span><span class="sxs-lookup"><span data-stu-id="20adf-127">For student enrollment dates, all of the web pages currently display the time along with the date, although all you care about for this field is the date.</span></span> <span data-ttu-id="20adf-128">使用資料註解屬性，您可以透過僅對一個程式碼進行變更，來修正每個顯示資料的檢視上的顯示格式。</span><span class="sxs-lookup"><span data-stu-id="20adf-128">By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.</span></span> <span data-ttu-id="20adf-129">為了查看如何進行此操作的範例，您將會新增一個屬性至 `Student` 類別中的 `EnrollmentDate` 屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-129">To see an example of how to do that, you'll add an attribute to the `EnrollmentDate` property in the `Student` class.</span></span>

<span data-ttu-id="20adf-130">在*Models\Student.cs*，新增`using`陳述式`System.ComponentModel.DataAnnotations`命名空間，並新增`DataType`並`DisplayFormat`屬性加入`EnrollmentDate`屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="20adf-130">In *Models\Student.cs*, add a `using` statement for the `System.ComponentModel.DataAnnotations` namespace and add `DataType` and `DisplayFormat` attributes to the `EnrollmentDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

<span data-ttu-id="20adf-131">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性用來指定比資料庫內建類型更特定的資料類型。</span><span class="sxs-lookup"><span data-stu-id="20adf-131">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="20adf-132">在此案例中，我們只想要追蹤日期，而非日期和時間。</span><span class="sxs-lookup"><span data-stu-id="20adf-132">In this case we only want to keep track of the date, not the date and time.</span></span> <span data-ttu-id="20adf-133">[DataType 列舉](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供許多資料類型，例如*日期、 時間、 PhoneNumber、 Currency、 EmailAddress*和更多功能。</span><span class="sxs-lookup"><span data-stu-id="20adf-133">The [DataType Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) provides for many data types, such as *Date, Time, PhoneNumber, Currency, EmailAddress* and more.</span></span> <span data-ttu-id="20adf-134">`DataType` 屬性也可讓應用程式自動提供類型的特定功能。</span><span class="sxs-lookup"><span data-stu-id="20adf-134">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="20adf-135">比方說，`mailto:`可以為建立連結[DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)，並可以針對提供的日期選擇器[DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)支援的瀏覽器[HTML5](http://html5.org/).</span><span class="sxs-lookup"><span data-stu-id="20adf-135">For example, a `mailto:` link can be created for [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), and a date selector can be provided for [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in browsers that support [HTML5](http://html5.org/).</span></span> <span data-ttu-id="20adf-136">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性會發出 HTML 5[資料集](http://ejohn.org/blog/html-5-data-attributes/)(phishing 英文發音如*data dash*) HTML 5 瀏覽器可以了解的屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-136">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes emits HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (pronounced *data dash*) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="20adf-137">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性不提供任何驗證。</span><span class="sxs-lookup"><span data-stu-id="20adf-137">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes do not provide any validation.</span></span>

<span data-ttu-id="20adf-138">`DataType.Date` 未指定顯示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="20adf-138">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="20adf-139">根據預設，server 為基礎的預設格式顯示資料欄位[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="20adf-139">By default, the data field is displayed according to the default formats based on the server's [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).</span></span>

<span data-ttu-id="20adf-140">`DisplayFormat` 屬性用來明確指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="20adf-140">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="20adf-141">`ApplyFormatInEditMode`設定可讓您指定，而指定的格式應該也會套用時的值會顯示在文字方塊中進行編輯。</span><span class="sxs-lookup"><span data-stu-id="20adf-141">The `ApplyFormatInEditMode` setting specifies that the specified formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="20adf-142">(您可能不想要的某些欄位 — 比方說，例如貨幣值，您可能不想在文字方塊中的貨幣符號進行編輯。)</span><span class="sxs-lookup"><span data-stu-id="20adf-142">(You might not want that for some fields — for example, for currency values, you might not want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="20adf-143">您可以使用[displayformat 無法](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性，但它通常是個不錯的主意，若要使用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)也屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-143">You can use the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute by itself, but it's generally a good idea to use the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute also.</span></span> <span data-ttu-id="20adf-144">`DataType`屬性會傳達*語意*的資料做為相對於如何呈現在螢幕上，並提供下列優點，就無法取得與`DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="20adf-144">The `DataType` attribute conveys the *semantics* of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with `DisplayFormat`:</span></span>

- <span data-ttu-id="20adf-145">瀏覽器可以啟用 HTML5 功能 (例如顯示日曆控制項、適合地區設定的貨幣符號、電子郵件連結、一些用戶端輸入驗證等等)。</span><span class="sxs-lookup"><span data-stu-id="20adf-145">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, some client-side input validation, etc.).</span></span>
- <span data-ttu-id="20adf-146">根據預設，瀏覽器會呈現資料使用正確的格式，根據您[地區設定](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20adf-146">By default, the browser will render data using the correct format based on your [locale](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).</span></span>
- <span data-ttu-id="20adf-147">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)屬性可以讓 MVC 選擇正確的欄位範本呈現的資料 ( [displayformat 無法](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)使用字串範本)。</span><span class="sxs-lookup"><span data-stu-id="20adf-147">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute can enable MVC to choose the right field template to render the data (the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) uses the string template).</span></span> <span data-ttu-id="20adf-148">如需詳細資訊，請參閱 Brad Wilson [ASP.NET MVC 2 範本](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="20adf-148">For more information, see Brad Wilson's [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="20adf-149">（針對 MVC 2 所撰寫，但這份文件仍適用於目前版本的 ASP.NET MVC。）</span><span class="sxs-lookup"><span data-stu-id="20adf-149">(Though written for MVC 2, this article still applies to the current version of ASP.NET MVC.)</span></span>

<span data-ttu-id="20adf-150">如果您使用`DataType`屬性與 [日期] 欄位中，您必須指定`DisplayFormat`也為了確保欄位在 Chrome 瀏覽器中正確轉譯的屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-150">If you use the `DataType` attribute with a date field, you have to specify the `DisplayFormat` attribute also in order to ensure that the field renders correctly in Chrome browsers.</span></span> <span data-ttu-id="20adf-151">如需詳細資訊，請參閱 <<c0> [ 這個 StackOverflow 執行緒](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。</span><span class="sxs-lookup"><span data-stu-id="20adf-151">For more information, see [this StackOverflow thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).</span></span>

<span data-ttu-id="20adf-152">如需如何處理在 MVC 中的其他日期格式的詳細資訊，請移至[MVC 5 簡介：檢查編輯方法與編輯檢視](../introduction/examining-the-edit-methods-and-edit-view.md)和 [搜尋] 中的頁面&quot;國際化&quot;。</span><span class="sxs-lookup"><span data-stu-id="20adf-152">For more information about how to handle other date formats in MVC, go to [MVC 5 Introduction: Examining the Edit Methods and Edit View](../introduction/examining-the-edit-methods-and-edit-view.md) and search in the page for &quot;internationalization&quot;.</span></span>

<span data-ttu-id="20adf-153">再次執行 學生的 索引 頁面，並請注意，時間都不會再顯示註冊日期欄位。</span><span class="sxs-lookup"><span data-stu-id="20adf-153">Run the Student Index page again and notice that times are no longer displayed for the enrollment dates.</span></span> <span data-ttu-id="20adf-154">也會使用任何檢視，則為 true`Student`模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-154">The same will be true for any view that uses the `Student` model.</span></span>

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a><span data-ttu-id="20adf-156">StringLengthAttribute</span><span class="sxs-lookup"><span data-stu-id="20adf-156">The StringLengthAttribute</span></span>

<span data-ttu-id="20adf-157">您也可以使用屬性指定資料驗證規則和驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="20adf-157">You can also specify data validation rules and validation error messages using attributes.</span></span> <span data-ttu-id="20adf-158">[StringLength 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)設定資料庫中的最大長度，並提供用戶端和伺服器端 ASP.NET mvc 的驗證。</span><span class="sxs-lookup"><span data-stu-id="20adf-158">The [StringLength attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) sets the maximum length in the database and provides client side and server side validation for ASP.NET MVC.</span></span> <span data-ttu-id="20adf-159">您也可以在此屬性中指定最小字串長度，但最小值不會對資料庫結構描述造成任何影響。</span><span class="sxs-lookup"><span data-stu-id="20adf-159">You can also specify the minimum string length in this attribute, but the minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="20adf-160">假設您想要確保使用者不會在名稱中輸入超過 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="20adf-160">Suppose you want to ensure that users don't enter more than 50 characters for a name.</span></span> <span data-ttu-id="20adf-161">若要新增這項限制，請新增[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性加入`LastName`和`FirstMidName`屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="20adf-161">To add this limitation, add [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attributes to the `LastName` and `FirstMidName` properties, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

<span data-ttu-id="20adf-162">[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性不會防止使用者名稱中輸入空白字元。</span><span class="sxs-lookup"><span data-stu-id="20adf-162">The [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute won't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="20adf-163">您可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)將限制套用至輸入的屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-163">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to apply restrictions to the input.</span></span> <span data-ttu-id="20adf-164">例如下列程式碼所需要的第一個字元必須是大寫，而其餘字元必須是英文字母：</span><span class="sxs-lookup"><span data-stu-id="20adf-164">For example the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

<span data-ttu-id="20adf-165">[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)屬性會提供類似的功能[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性，但並不提供用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="20adf-165">The [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) attribute provides similar functionality to the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute but doesn't provide client side validation.</span></span>

<span data-ttu-id="20adf-166">執行應用程式，然後按一下**學生** 索引標籤。您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="20adf-166">Run the application and click the **Students** tab. You get the following error:</span></span>

<span data-ttu-id="20adf-167">*備份 'SchoolContext' 內容的模型已變更，因為所建立的資料庫。請考慮使用 Code First 移轉更新資料庫 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。*</span><span class="sxs-lookup"><span data-stu-id="20adf-167">*The model backing the 'SchoolContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*</span></span>

<span data-ttu-id="20adf-168">資料庫模型已變更，需要變更資料庫結構描述中，Entity Framework 偵測到。</span><span class="sxs-lookup"><span data-stu-id="20adf-168">The database model has changed in a way that requires a change in the database schema, and Entity Framework detected that.</span></span> <span data-ttu-id="20adf-169">您將使用移轉，而不會遺失任何您使用 UI 新增到資料庫的資料更新結構描述。</span><span class="sxs-lookup"><span data-stu-id="20adf-169">You'll use migrations to update the schema without losing any data that you added to the database by using the UI.</span></span> <span data-ttu-id="20adf-170">如果您變更所建立的資料`Seed`方法，將會變更回其原始狀態，因為[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)您在中使用的方法`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="20adf-170">If you changed data that was created by the `Seed` method, that will be changed back to its original state because of the [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) method that you're using in the `Seed` method.</span></span> <span data-ttu-id="20adf-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)相當於"upsert"作業從資料庫詞彙中。)</span><span class="sxs-lookup"><span data-stu-id="20adf-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) is equivalent to an "upsert" operation from database terminology.)</span></span>

<span data-ttu-id="20adf-172">請在套件管理員主控台 (PMC) 中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="20adf-172">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

<span data-ttu-id="20adf-173">`add-migration`命令會建立名為的檔案 *&lt;時間戳記&gt;\_MaxLengthOnNames.cs* 。</span><span class="sxs-lookup"><span data-stu-id="20adf-173">The `add-migration` command creates a file named *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*.</span></span> <span data-ttu-id="20adf-174">此檔案包含了 `Up` 方法中的程式碼，可更新資料庫，使其符合目前的資料模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-174">This file contains code in the `Up` method that will update the database to match the current data model.</span></span> <span data-ttu-id="20adf-175">`update-database` 命令執行了該程式碼。</span><span class="sxs-lookup"><span data-stu-id="20adf-175">The `update-database` command ran that code.</span></span>

<span data-ttu-id="20adf-176">Entity Framework 會使用移轉檔案名稱的前面加上時間戳記來排序移轉。</span><span class="sxs-lookup"><span data-stu-id="20adf-176">The timestamp prepended to the migrations file name is used by Entity Framework to order the migrations.</span></span> <span data-ttu-id="20adf-177">您可以建立多個移轉前執行`update-database`命令，然後所有的移轉會套用已建立的順序。</span><span class="sxs-lookup"><span data-stu-id="20adf-177">You can create multiple migrations before running the `update-database` command, and then all of the migrations are applied in the order in which they were created.</span></span>

<span data-ttu-id="20adf-178">執行**建立**頁面，然後輸入超過 50 個字元名稱。</span><span class="sxs-lookup"><span data-stu-id="20adf-178">Run the **Create** page, and enter either name longer than 50 characters.</span></span> <span data-ttu-id="20adf-179">當您按一下 **建立**，用戶端驗證便會顯示錯誤訊息：*LastName 欄位必須是具有最大長度為 50 的字串。*</span><span class="sxs-lookup"><span data-stu-id="20adf-179">When you click **Create**, client side validation shows an error message: *The field LastName must be a string with a maximum length of 50.*</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="20adf-180">資料行屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-180">The Column Attribute</span></span>

<span data-ttu-id="20adf-181">您也可以使用屬性控制您的類別和屬性對應到資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="20adf-181">You can also use attributes to control how your classes and properties are mapped to the database.</span></span> <span data-ttu-id="20adf-182">假設您已針對名字欄位使用 `FirstMidName` 作為名稱，因為欄位中可能也會包含中間名。</span><span class="sxs-lookup"><span data-stu-id="20adf-182">Suppose you had used the name `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span> <span data-ttu-id="20adf-183">但您想要將資料庫資料行命名為 `FirstName`，因為撰寫臨機操作查詢資料庫的使用者比較習慣該名稱。</span><span class="sxs-lookup"><span data-stu-id="20adf-183">But you want the database column to be named `FirstName`, because users who will be writing ad-hoc queries against the database are accustomed to that name.</span></span> <span data-ttu-id="20adf-184">若要進行此對應，您可以使用 `Column` 屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-184">To make this mapping, you can use the `Column` attribute.</span></span>

<span data-ttu-id="20adf-185">`Column` 屬性指定當建立資料庫時，`Student` 資料表中對應到 `FirstMidName` 屬性的資料行會命名為 `FirstName`。</span><span class="sxs-lookup"><span data-stu-id="20adf-185">The `Column` attribute specifies that when the database is created, the column of the `Student` table that maps to the `FirstMidName` property will be named `FirstName`.</span></span> <span data-ttu-id="20adf-186">換句話說，當您的程式碼參照 `Student.FirstMidName` 時，資料便會來自 `Student` 資料表中的 `FirstName` 資料行或在其中更新。</span><span class="sxs-lookup"><span data-stu-id="20adf-186">In other words, when your code refers to `Student.FirstMidName`, the data will come from or be updated in the `FirstName` column of the `Student` table.</span></span> <span data-ttu-id="20adf-187">如果您未指定資料行名稱，就會提供相同的名稱與屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="20adf-187">If you don't specify column names, they are given the same name as the property name.</span></span>

<span data-ttu-id="20adf-188">在  *Student.cs*檔案中，新增`using`陳述式[System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)並加入資料行名稱屬性來`FirstMidName`屬性中所示下列醒目提示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-188">In the *Student.cs* file, add a `using` statement for [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) and add the column name attribute to the `FirstMidName` property, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

<span data-ttu-id="20adf-189">新增[資料行屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)變更備份 SchoolContext，因此它不會符合資料庫的模型。</span><span class="sxs-lookup"><span data-stu-id="20adf-189">The addition of the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) changes the model backing the SchoolContext, so it won't match the database.</span></span> <span data-ttu-id="20adf-190">在 PMC 中建立另一個移轉，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="20adf-190">Enter the following commands in the PMC to create another migration:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

<span data-ttu-id="20adf-191">在 **伺服器總管**，開啟*學生*資料表設計工具，按兩下*學生*資料表。</span><span class="sxs-lookup"><span data-stu-id="20adf-191">In **Server Explorer**, open the *Student* table designer by double-clicking the *Student* table.</span></span>

<span data-ttu-id="20adf-192">您套用前兩個移轉之前下, 圖顯示原始的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="20adf-192">The following image shows the original column name as it was before you applied the first two migrations.</span></span> <span data-ttu-id="20adf-193">除了從變更資料行名稱`FirstMidName`要`FirstName`，兩個名稱的資料行已從`MAX`長度為 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="20adf-193">In addition to the column name changing from `FirstMidName` to `FirstName`, the two name columns have changed from `MAX` length to 50 characters.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="20adf-194">您也可以進行資料庫使用的對應變更[Fluent API](https://msdn.microsoft.com/data/jj591617)，如本教學課程稍後，您會看到。</span><span class="sxs-lookup"><span data-stu-id="20adf-194">You can also make database mapping changes using the [Fluent API](https://msdn.microsoft.com/data/jj591617), as you'll see later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="20adf-195">若您嘗試在完成建立下列章節中所有的實體類別前進行編譯，您可能會收到編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="20adf-195">If you try to compile before you finish creating all of the entity classes in the following sections, you might get compiler errors.</span></span>

## <a name="update-student-entity"></a><span data-ttu-id="20adf-196">更新 Student 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-196">Update Student entity</span></span>

<span data-ttu-id="20adf-197">在  *Models\Student.cs*，稍早為下列程式碼取代您所新增的程式碼。</span><span class="sxs-lookup"><span data-stu-id="20adf-197">In *Models\Student.cs*, replace the code you added earlier with the following code.</span></span> <span data-ttu-id="20adf-198">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="20adf-198">The changes are highlighted.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a><span data-ttu-id="20adf-199">必要的屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-199">The Required Attribute</span></span>

<span data-ttu-id="20adf-200">[必要的屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)讓名稱屬性的必要的欄位。</span><span class="sxs-lookup"><span data-stu-id="20adf-200">The [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) makes the name properties required fields.</span></span> <span data-ttu-id="20adf-201">`Required attribute`不需要使用實值型別，例如 DateTime、 int、 double、 和 float。</span><span class="sxs-lookup"><span data-stu-id="20adf-201">The `Required attribute` is not needed for value types such as DateTime, int, double, and float.</span></span> <span data-ttu-id="20adf-202">實值型別不能指定 null 值，因此原本就視為必要欄位。</span><span class="sxs-lookup"><span data-stu-id="20adf-202">Value types cannot be assigned a null value, so they are inherently treated as required fields.</span></span> <span data-ttu-id="20adf-203">您也可以移除[必要的屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)，並使用的最小長度參數取代`StringLength`屬性：</span><span class="sxs-lookup"><span data-stu-id="20adf-203">You could remove the [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) and replace it with a minimum length parameter for the `StringLength` attribute:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

### <a name="the-display-attribute"></a><span data-ttu-id="20adf-204">顯示屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-204">The Display Attribute</span></span>

<span data-ttu-id="20adf-205">`Display` 屬性指定了文字方塊的標題應為「名字」、「姓氏」、「全名」及「註冊日期」，而非每個執行個體中的屬性名稱 (沒有使用空格鍵分隔單字的名稱)。</span><span class="sxs-lookup"><span data-stu-id="20adf-205">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date" instead of the property name in each instance (which has no space dividing the words).</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="20adf-206">FullName 計算屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-206">The FullName Calculated Property</span></span>

<span data-ttu-id="20adf-207">`FullName` 為一個計算屬性，會傳回藉由串連兩個其他屬性而建立的值。</span><span class="sxs-lookup"><span data-stu-id="20adf-207">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="20adf-208">因此只有`get`存取子，且沒有`FullName`會產生資料庫中的資料行。</span><span class="sxs-lookup"><span data-stu-id="20adf-208">Therefore it has only a `get` accessor, and no `FullName` column will be generated in the database.</span></span>

## <a name="create-instructor-entity"></a><span data-ttu-id="20adf-209">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-209">Create Instructor entity</span></span>

<span data-ttu-id="20adf-210">建立*Models\Instructor.cs*，以下列程式碼取代範本程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-210">Create *Models\Instructor.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="20adf-211">請注意，當中有幾個屬性跟 `Student` 和 `Instructor` 實體中的一樣。</span><span class="sxs-lookup"><span data-stu-id="20adf-211">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="20adf-212">在本系列稍後的[實作繼承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中，您會對此程式碼進行重構以消除冗餘。</span><span class="sxs-lookup"><span data-stu-id="20adf-212">In the [Implementing Inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series, you'll refactor this code to eliminate the redundancy.</span></span>

<span data-ttu-id="20adf-213">您可以將多個屬性放在同一行，因此您也可以如下撰寫 instructor 類別：</span><span class="sxs-lookup"><span data-stu-id="20adf-213">You can put multiple attributes on one line, so you could also write the instructor class as follows:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a><span data-ttu-id="20adf-214">課程和 OfficeAssignment 導覽屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-214">The Courses and OfficeAssignment Navigation Properties</span></span>

<span data-ttu-id="20adf-215">`Courses` 和 `OfficeAssignment` 屬性為導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-215">The `Courses` and `OfficeAssignment` properties are navigation properties.</span></span> <span data-ttu-id="20adf-216">如已先前所述，它們通常會定義為[虛擬](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx)，讓他們可以利用稱為 Entity Framework 功能[消極式載入](https://msdn.microsoft.com/magazine/hh205756.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20adf-216">As was explained earlier, they are typically defined as [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) so that they can take advantage of an Entity Framework feature called [lazy loading](https://msdn.microsoft.com/magazine/hh205756.aspx).</span></span> <span data-ttu-id="20adf-217">此外，如果導覽屬性可以保存多個實體，其類型必須實作[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)介面。</span><span class="sxs-lookup"><span data-stu-id="20adf-217">In addition, if a navigation property can hold multiple entities, its type must implement the [ICollection&lt;T&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface.</span></span> <span data-ttu-id="20adf-218">比方說[IList&lt;T&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)而非限定[IEnumerable&lt;T&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx)因為`IEnumerable<T>`不實作[新增](https://msdn.microsoft.com/library/63ywd54z.aspx).</span><span class="sxs-lookup"><span data-stu-id="20adf-218">For example [IList&lt;T&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifies but not [IEnumerable&lt;T&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) because `IEnumerable<T>` doesn't implement [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).</span></span>

<span data-ttu-id="20adf-219">講師可以教授任何數量的課程，因此`Courses`定義為集合`Course`實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-219">An instructor can teach any number of courses, so `Courses` is defined as a collection of `Course` entities.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="20adf-220">我們的商務規則狀態講師只可以有最多一個辦公室，因此`OfficeAssignment`定義為單一`OfficeAssignment`實體 (這可能是`null`如果被不指派任何辦公室)。</span><span class="sxs-lookup"><span data-stu-id="20adf-220">Our business rules state an instructor can only have at most one office, so `OfficeAssignment` is defined as a single `OfficeAssignment` entity (which may be `null` if no office is assigned).</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a><span data-ttu-id="20adf-221">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-221">Create OfficeAssignment entity</span></span>

<span data-ttu-id="20adf-222">建立*Models\OfficeAssignment.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-222">Create *Models\OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="20adf-223">建置專案時，會將儲存您的變更，並確認您未進行任何複製並貼上，編譯器可以攔截的錯誤。</span><span class="sxs-lookup"><span data-stu-id="20adf-223">Build the project, which saves your changes and verifies you haven't made any copy and paste errors the compiler can catch.</span></span>

### <a name="the-key-attribute"></a><span data-ttu-id="20adf-224">索引鍵屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-224">The Key Attribute</span></span>

<span data-ttu-id="20adf-225">-0-或-一對一關聯性之間`Instructor`而`OfficeAssignment`實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-225">There's a one-to-zero-or-one relationship between the `Instructor` and the `OfficeAssignment` entities.</span></span> <span data-ttu-id="20adf-226">辦公室指派只存在於，它指派的講師，因此其主索引鍵也是其外部索引鍵`Instructor`實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-226">An office assignment only exists in relation to the instructor it's assigned to, and therefore its primary key is also its foreign key to the `Instructor` entity.</span></span> <span data-ttu-id="20adf-227">但 Entity Framework 無法自動辨識`InstructorID`做為主要索引鍵的實體因為其名稱並未遵循`ID`或*classname* `ID`命名慣例。</span><span class="sxs-lookup"><span data-stu-id="20adf-227">But the Entity Framework can't automatically recognize `InstructorID` as the primary key of this entity because its name doesn't follow the `ID` or *classname* `ID` naming convention.</span></span> <span data-ttu-id="20adf-228">因此，必須使用 `Key` 屬性將其識別為 PK：</span><span class="sxs-lookup"><span data-stu-id="20adf-228">Therefore, the `Key` attribute is used to identify it as the key:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="20adf-229">您也可以使用`Key`屬性，若實體確實有它自己的主索引鍵，但您想要命名為不同名稱的屬性`classnameID`或`ID`。</span><span class="sxs-lookup"><span data-stu-id="20adf-229">You can also use the `Key` attribute if the entity does have its own primary key but you want to name the property something different than `classnameID` or `ID`.</span></span> <span data-ttu-id="20adf-230">根據預設 EF 會作為非資料庫產生將索引鍵，因為資料行是用於識別關聯性。</span><span class="sxs-lookup"><span data-stu-id="20adf-230">By default EF treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-foreignkey-attribute"></a><span data-ttu-id="20adf-231">ForeignKey 屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-231">The ForeignKey Attribute</span></span>

<span data-ttu-id="20adf-232">-0-或-一對一關聯性或兩個實體之間的一對一關聯性時 (這類之間`OfficeAssignment`和`Instructor`)，EF 就出關聯性的一端是主體和相依的結束，即無法運作。</span><span class="sxs-lookup"><span data-stu-id="20adf-232">When there is a one-to-zero-or-one relationship or a one-to-one relationship between two entities (such as between `OfficeAssignment` and `Instructor`), EF can't work out which end of the relationship is the principal and which end is dependent.</span></span> <span data-ttu-id="20adf-233">一對一關聯性會在每個類別與其他類別中的參考導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-233">One-to-one relationships have a reference navigation property in each class to the other class.</span></span> <span data-ttu-id="20adf-234">[ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可以套用至相依的類別，以建立關聯性。</span><span class="sxs-lookup"><span data-stu-id="20adf-234">The [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) can be applied to the dependent class to establish the relationship.</span></span> <span data-ttu-id="20adf-235">如果您省略[ForeignKey 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)，當您嘗試建立移轉作業時，收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="20adf-235">If you omit the [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), you get the following error when you try to create the migration:</span></span>

<span data-ttu-id="20adf-236">*無法判斷 'ContosoUniversity.Models.OfficeAssignment' 和 'ContosoUniversity.Models.Instructor' 類型間之關聯的主要末端。此關聯的主體端點必須明確地設定使用的關聯性的 fluent API 」 或 「 資料註解。*</span><span class="sxs-lookup"><span data-stu-id="20adf-236">*Unable to determine the principal end of an association between the types 'ContosoUniversity.Models.OfficeAssignment' and 'ContosoUniversity.Models.Instructor'. The principal end of this association must be explicitly configured using either the relationship fluent API or data annotations.*</span></span>

<span data-ttu-id="20adf-237">稍後在本教學課程中，您會看到如何使用 fluent API 設定此關聯性。</span><span class="sxs-lookup"><span data-stu-id="20adf-237">Later in the tutorial you'll see how to configure this relationship with the fluent API.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="20adf-238">Instructor 導覽屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-238">The Instructor Navigation Property</span></span>

<span data-ttu-id="20adf-239">`Instructor`實體具有可為 null`OfficeAssignment`導覽屬性 （因為一名講師可能沒有辦公室指派），而`OfficeAssignment`實體有不可為 null`Instructor`導覽屬性 （因為辦公室指派無法講師-之外存在`InstructorID`不可為 null)。</span><span class="sxs-lookup"><span data-stu-id="20adf-239">The `Instructor` entity has a nullable `OfficeAssignment` navigation property (because an instructor might not have an office assignment), and the `OfficeAssignment` entity has a non-nullable `Instructor` navigation property (because an office assignment can't exist without an instructor -- `InstructorID` is non-nullable).</span></span> <span data-ttu-id="20adf-240">當`Instructor`實體有相關`OfficeAssignment`實體，每個實體會有另一個在其導覽屬性中的參考。</span><span class="sxs-lookup"><span data-stu-id="20adf-240">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity will have a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="20adf-241">您可以將放入`[Required]`上 Instructor 導覽屬性，指定必須有一個相關的講師，但您不需要這麼做，因為 InstructorID 外部索引鍵 （這也是這個資料表的索引鍵） 是不可為 null 的屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-241">You could put a `[Required]` attribute on the Instructor navigation property to specify that there must be a related instructor, but you don't have to do that because the InstructorID foreign key (which is also the key to this table) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="20adf-242">修改 Course 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-242">Modify the Course entity</span></span>

<span data-ttu-id="20adf-243">在  *Models\Course.cs*，稍早為下列程式碼取代您所新增的程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-243">In *Models\Course.cs*, replace the code you added earlier with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="20adf-244">Course 實體具有外部索引鍵屬性`DepartmentID`指向相關`Department`實體，且具有`Department`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-244">The course entity has a foreign key property `DepartmentID` which points to the related `Department` entity and it has a `Department` navigation property.</span></span> <span data-ttu-id="20adf-245">當您針對相關實體具有一個導覽屬性時，Entity Framework 便不需要您為資料模型新增一個外部索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-245">The Entity Framework doesn't require you to add a foreign key property to your data model when you have a navigation property for a related entity.</span></span> <span data-ttu-id="20adf-246">在需要時會，EF 會將外部索引鍵會自動建立資料庫中。</span><span class="sxs-lookup"><span data-stu-id="20adf-246">EF automatically creates foreign keys in the database wherever they are needed.</span></span> <span data-ttu-id="20adf-247">但在資料模型中擁有外部索引鍵，可讓更新變得更為簡單和有效率。</span><span class="sxs-lookup"><span data-stu-id="20adf-247">But having the foreign key in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="20adf-248">例如，當擷取課程實體，若要編輯，時才`Department`實體為 null 如果您沒有載入它，因此當您更新課程實體，您必須先擷取`Department`實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-248">For example, when you fetch a course entity to edit, the `Department` entity is null if you don't load it, so when you update the course entity, you would have to first fetch the `Department` entity.</span></span> <span data-ttu-id="20adf-249">當外部索引鍵的屬性`DepartmentID`是否包含在資料模型中，您不需要擷取`Department`才能更新的實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-249">When the foreign key property `DepartmentID` is included in the data model, you don't need to fetch the `Department` entity before you update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="20adf-250">DatabaseGenerated 屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-250">The DatabaseGenerated Attribute</span></span>

<span data-ttu-id="20adf-251">[DatabaseGenerated 屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)具有[無](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)參數`CourseID`屬性指定主索引鍵值是使用者所提供，而非資料庫產生的。</span><span class="sxs-lookup"><span data-stu-id="20adf-251">The [DatabaseGenerated attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) with the [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parameter on the `CourseID` property specifies that primary key values are provided by the user rather than generated by the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="20adf-252">根據預設，Entity Framework 會假設主索引鍵值由資料庫產生。</span><span class="sxs-lookup"><span data-stu-id="20adf-252">By default, the Entity Framework assumes that primary key values are generated by the database.</span></span> <span data-ttu-id="20adf-253">這是您在大多數案例下所希望的情況。</span><span class="sxs-lookup"><span data-stu-id="20adf-253">That's what you want in most scenarios.</span></span> <span data-ttu-id="20adf-254">不過，對於`Course`實體，您會使用使用者指定的課程號碼 1000年系列的一個部門，另一個部門，使用 2000年系列等等。</span><span class="sxs-lookup"><span data-stu-id="20adf-254">However, for `Course` entities, you'll use a user-specified course number such as a 1000 series for one department, a 2000 series for another department, and so on.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="20adf-255">外部索引鍵及導覽屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-255">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="20adf-256">外部索引鍵屬性和導覽屬性在`Course`實體反映了下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="20adf-256">The foreign key properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

- <span data-ttu-id="20adf-257">課程會指派給一個部門，因此基於上述理由，會有一個 `DepartmentID` 外部索引鍵和一個 `Department` 導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-257">A course is assigned to one department, so there's a `DepartmentID` foreign key and a `Department` navigation property for the reasons mentioned above.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- <span data-ttu-id="20adf-258">由於課程可由任何數量的學生進行註冊，因此 `Enrollments` 導覽屬性為一個集合：</span><span class="sxs-lookup"><span data-stu-id="20adf-258">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- <span data-ttu-id="20adf-259">課程可由多個講師進行教授，因此 `Instructors` 導覽屬性為一個集合：</span><span class="sxs-lookup"><span data-stu-id="20adf-259">A course may be taught by multiple instructors, so the `Instructors` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a><span data-ttu-id="20adf-260">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-260">Create the Department entity</span></span>

<span data-ttu-id="20adf-261">建立*Models\Department.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-261">Create *Models\Department.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a><span data-ttu-id="20adf-262">資料行屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-262">The Column Attribute</span></span>

<span data-ttu-id="20adf-263">您使用稍早[資料行屬性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)來變更資料行名稱對應。</span><span class="sxs-lookup"><span data-stu-id="20adf-263">Earlier you used the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) to change column name mapping.</span></span> <span data-ttu-id="20adf-264">在程式碼`Department`實體，`Column`屬性用來變更 SQL 資料類型對應，以便使用 SQL Server 就會定義資料行[money](https://msdn.microsoft.com/library/ms179882.aspx)資料庫中的型別：</span><span class="sxs-lookup"><span data-stu-id="20adf-264">In the code for the `Department` entity, the `Column` attribute is being used to change SQL data type mapping so that the column will be defined using the SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) type in the database:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="20adf-265">資料行對應通常是不必要的因為 Entity Framework 通常會選擇根據您定義屬性的 CLR 類型的適當 SQL Server 資料類型。</span><span class="sxs-lookup"><span data-stu-id="20adf-265">Column mapping is generally not required, because the Entity Framework usually chooses the appropriate SQL Server data type based on the CLR type that you define for the property.</span></span> <span data-ttu-id="20adf-266">CLR `decimal` 類型會對應到 SQL Server 的 `decimal` 類型。</span><span class="sxs-lookup"><span data-stu-id="20adf-266">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="20adf-267">但在此情況下您知道資料行，將會儲存貨幣數量，而[金錢](https://msdn.microsoft.com/library/ms179882.aspx)資料類型是最適合的。</span><span class="sxs-lookup"><span data-stu-id="20adf-267">But in this case you know that the column will be holding currency amounts, and the [money](https://msdn.microsoft.com/library/ms179882.aspx) data type is more appropriate for that.</span></span> <span data-ttu-id="20adf-268">如需有關 CLR 資料類型，且它們如何符合 SQL Server 資料類型的詳細資訊，請參閱 <<c0> [ 適用於 Entity framework 的 sqlclient 類型 SqlClient](https://msdn.microsoft.com/library/bb896344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="20adf-268">For more information about CLR data types and how they match to SQL Server data types, see [SqlClient for Entity FrameworkTypes](https://msdn.microsoft.com/library/bb896344.aspx).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="20adf-269">外部索引鍵及導覽屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-269">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="20adf-270">外部索引鍵及導覽屬性反映了下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="20adf-270">The foreign key and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="20adf-271">部門可以有或沒有一位系統管理員，而系統管理員一律為講師。</span><span class="sxs-lookup"><span data-stu-id="20adf-271">A department may or may not have an administrator, and an administrator is always an instructor.</span></span> <span data-ttu-id="20adf-272">因此`InstructorID`屬性是包含做為外部索引鍵`Instructor`後面會加上實體，以及使用問號`int`類型標示為可為 null 的該屬性指定。導覽屬性名為`Administrator`但保留`Instructor`實體：</span><span class="sxs-lookup"><span data-stu-id="20adf-272">Therefore the `InstructorID` property is included as the foreign key to the `Instructor` entity, and a question mark is added after the `int` type designation to mark the property as nullable.The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- <span data-ttu-id="20adf-273">部門中可能包含許多課程，因此沒有`Courses`導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="20adf-273">A department may have many courses, so there's a `Courses` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > <span data-ttu-id="20adf-274">根據慣例，Entity Framework 會為不可為 Null 的外部索引鍵和多對多關聯性啟用串聯刪除。</span><span class="sxs-lookup"><span data-stu-id="20adf-274">By convention, the Entity Framework enables cascade delete for non-nullable foreign keys and for many-to-many relationships.</span></span> <span data-ttu-id="20adf-275">這可能會導致循環串聯刪除規則，並在您嘗試新增移轉時造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="20adf-275">This can result in circular cascade delete rules, which will cause an exception when you try to add a migration.</span></span> <span data-ttu-id="20adf-276">例如，如果您未定義`Department.InstructorID`屬性可為 null，您會收到下列例外狀況訊息：「 參考關聯性將會導致不允許循環參考。 」</span><span class="sxs-lookup"><span data-stu-id="20adf-276">For example, if you didn't define the `Department.InstructorID` property as nullable, you'd get the following exception message: "The referential relationship will result in a cyclical reference that's not allowed."</span></span> <span data-ttu-id="20adf-277">如果您的商務規則所需`InstructorID`屬性成為不可為 null，您必須使用下列 fluent API 陳述式停用串聯刪除關聯性：</span><span class="sxs-lookup"><span data-stu-id="20adf-277">If your business rules required `InstructorID` property to be non-nullable, you would have to use the following fluent API statement to disable cascade delete on the relationship:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a><span data-ttu-id="20adf-278">修改 Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-278">Modify the Enrollment entity</span></span>

 <span data-ttu-id="20adf-279">在  *Models\Enrollment.cs*，稍早為下列程式碼取代您所新增的程式碼</span><span class="sxs-lookup"><span data-stu-id="20adf-279">In *Models\Enrollment.cs*, replace the code you added earlier with the following code</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="20adf-280">外部索引鍵及導覽屬性</span><span class="sxs-lookup"><span data-stu-id="20adf-280">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="20adf-281">外部索引鍵屬性及導覽屬性反映了下列關聯性：</span><span class="sxs-lookup"><span data-stu-id="20adf-281">The foreign key properties and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="20adf-282">註冊記錄乃針對單一課程，因此當中包含了一個 `CourseID` 外部索引鍵屬性及一個 `Course` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="20adf-282">An enrollment record is for a single course, so there's a `CourseID` foreign key property and a `Course` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- <span data-ttu-id="20adf-283">註冊記錄乃針對單一學生，因此當中包含了一個 `StudentID` 外部索引鍵屬性及一個 `Student` 導覽屬性：</span><span class="sxs-lookup"><span data-stu-id="20adf-283">An enrollment record is for a single student, so there's a `StudentID` foreign key property and a `Student` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a><span data-ttu-id="20adf-284">多對多關聯性</span><span class="sxs-lookup"><span data-stu-id="20adf-284">Many-to-Many Relationships</span></span>

<span data-ttu-id="20adf-285">之間多對多關聯性`Student`和`Course`實體，而`Enrollment`實體的功能為多對多聯結資料表*承載*資料庫中。</span><span class="sxs-lookup"><span data-stu-id="20adf-285">There's a many-to-many relationship between the `Student` and `Course` entities, and the `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="20adf-286">這表示`Enrollment`資料表包含額外的資料，除了聯結資料表的外部索引鍵 (在此情況下，主索引鍵和`Grade`屬性)。</span><span class="sxs-lookup"><span data-stu-id="20adf-286">This means that the `Enrollment` table contains additional data besides foreign keys for the joined tables (in this case, a primary key and a `Grade` property).</span></span>

<span data-ttu-id="20adf-287">下列圖例展示了在實體圖表中這些關聯性的樣子。</span><span class="sxs-lookup"><span data-stu-id="20adf-287">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="20adf-288">(此圖表使用來產生[Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); 建立圖表不屬於本教學課程，只是正在使用它作為。)</span><span class="sxs-lookup"><span data-stu-id="20adf-288">(This diagram was generated using the [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); creating the diagram isn't part of the tutorial, it's just being used here as an illustration.)</span></span>

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="20adf-290">每個關聯性線條的一端，星號 1 (\*)，顯示其表示一個對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="20adf-290">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="20adf-291">如果`Enrollment`資料表並未包含成績資訊，其便只需要包含兩個外部索引鍵`CourseID`和`StudentID`。</span><span class="sxs-lookup"><span data-stu-id="20adf-291">If the `Enrollment` table didn't include grade information, it would only need to contain the two foreign keys `CourseID` and `StudentID`.</span></span> <span data-ttu-id="20adf-292">在此情況下，它就會對應至多對多聯結資料表*不具有承載*(或*純聯結資料表*) 資料庫中，您不需要完全為其建立的模型類別。</span><span class="sxs-lookup"><span data-stu-id="20adf-292">In that case, it would correspond to a many-to-many join table *without payload* (or a *pure join table*) in the database, and you wouldn't have to create a model class for it at all.</span></span> <span data-ttu-id="20adf-293">`Instructor`和`Course`實體具有此類型的多對多關聯性，並如您所見，它們之間沒有實體類別：</span><span class="sxs-lookup"><span data-stu-id="20adf-293">The `Instructor` and `Course` entities have that kind of many-to-many relationship, and as you can see, there is no entity class between them:</span></span>

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="20adf-295">聯結資料表，才在資料庫中，不過，在下列的資料庫圖表所示：</span><span class="sxs-lookup"><span data-stu-id="20adf-295">A join table is required in the database, however, as shown in the following database diagram:</span></span>

![Instructor-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="20adf-297">Entity Framework 會自動建立`CourseInstructor`資料表，以及您讀取和更新的讀取和更新的間接`Instructor.Courses`和`Course.Instructors`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-297">The Entity Framework automatically creates the `CourseInstructor` table, and you read and update it indirectly by reading and updating the `Instructor.Courses` and `Course.Instructors` navigation properties.</span></span>

## <a name="entity-relationship-diagram"></a><span data-ttu-id="20adf-298">實體關係圖</span><span class="sxs-lookup"><span data-stu-id="20adf-298">Entity relationship diagram</span></span>

<span data-ttu-id="20adf-299">下列圖例顯示了 Entity Framework Power Tools 為完成的 School 模型建立的圖表。</span><span class="sxs-lookup"><span data-stu-id="20adf-299">The following illustration shows the diagram that the Entity Framework Power Tools create for the completed School model.</span></span>

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="20adf-301">除了多對多關聯性線條 (\*來\*) 和一對多關聯性線條 (1 到\*)，您可以看到以下到零或-一一關聯性線條 (1 對 0..1) 之間`Instructor`和`OfficeAssignment`實體和零-或--一對多關聯性線條 (0..1 對\*) 之間的 Instructor 和 Department 實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-301">Besides the many-to-many relationship lines (\* to \*) and the one-to-many relationship lines (1 to \*), you can see here the one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities and the zero-or-one-to-many relationship line (0..1 to \*) between the Instructor and Department entities.</span></span>

## <a name="add-code-to-database-context"></a><span data-ttu-id="20adf-302">將程式碼加入至資料庫的內容</span><span class="sxs-lookup"><span data-stu-id="20adf-302">Add code to database context</span></span>

<span data-ttu-id="20adf-303">接下來您要在其中加入新的實體來`SchoolContext`類別，並自訂對應使用的一些[fluent API](https://msdn.microsoft.com/data/jj591617)呼叫。</span><span class="sxs-lookup"><span data-stu-id="20adf-303">Next you'll add the new entities to the `SchoolContext` class and customize some of the mapping using [fluent API](https://msdn.microsoft.com/data/jj591617) calls.</span></span> <span data-ttu-id="20adf-304">API 是"fluent"，因為它通常由串連一系列的方法呼叫一起成單一陳述式，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="20adf-304">The API is "fluent" because it's often used by stringing a series of method calls together into a single statement, as in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

<span data-ttu-id="20adf-305">在本教學課程中，您將使用 fluent API 僅針對您無法使用屬性操作的資料庫對應。</span><span class="sxs-lookup"><span data-stu-id="20adf-305">In this tutorial you'll use the fluent API only for database mapping that you can't do with attributes.</span></span> <span data-ttu-id="20adf-306">然而，您也可以使用 Fluent API 指定大部分透過屬性可完成的格式、驗證及對應規則。</span><span class="sxs-lookup"><span data-stu-id="20adf-306">However, you can also use the fluent API to specify most of the formatting, validation, and mapping rules that you can do by using attributes.</span></span> <span data-ttu-id="20adf-307">某些屬性 (例如 `MinimumLength`) 無法使用 Fluent API 來套用。</span><span class="sxs-lookup"><span data-stu-id="20adf-307">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="20adf-308">如前所述，`MinimumLength`不會變更結構描述，它只適用於用戶端和伺服器端驗證規則</span><span class="sxs-lookup"><span data-stu-id="20adf-308">As mentioned previously, `MinimumLength` doesn't change the schema, it only applies a client and server side validation rule</span></span>

<span data-ttu-id="20adf-309">某些開發人員偏好單獨使用 Fluent API，使其實體類別保持「整潔」。</span><span class="sxs-lookup"><span data-stu-id="20adf-309">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="20adf-310">若想要的話，您也可以混合使用屬性和 Fluent API，並且有一些自訂項目只能使用 Fluent API 完成。但一般來說，建議的做法是在這兩種方法中選擇其中一項，然後盡可能的一致使用該方法。</span><span class="sxs-lookup"><span data-stu-id="20adf-310">You can mix attributes and fluent API if you want, and there are a few customizations that can only be done by using fluent API, but in general the recommended practice is to choose one of these two approaches and use that consistently as much as possible.</span></span>

<span data-ttu-id="20adf-311">若要加入新的實體資料模型，並執行您未使用屬性的資料庫對應，取代中的程式碼*DAL\SchoolContext.cs*為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="20adf-311">To add the new entities to the data model and perform database mapping that you didn't do by using attributes, replace the code in *DAL\SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="20adf-312">在新的陳述式[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法設定多對多聯結資料表：</span><span class="sxs-lookup"><span data-stu-id="20adf-312">The new statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method configures the many-to-many join table:</span></span>

- <span data-ttu-id="20adf-313">多對多關聯性之間`Instructor`和`Course`實體，程式碼指定聯結資料表的資料表和資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="20adf-313">For the many-to-many relationship between the `Instructor` and `Course` entities, the code specifies the table and column names for the join table.</span></span> <span data-ttu-id="20adf-314">程式碼第一次可以設定多對多關聯性，而不需要這個程式碼，但如果您未呼叫它，就會預設名稱這類`InstructorInstructorID`針對`InstructorID`資料行。</span><span class="sxs-lookup"><span data-stu-id="20adf-314">Code First can configure the many-to-many relationship for you without this code, but if you don't call it, you will get default names such as `InstructorInstructorID` for the `InstructorID` column.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="20adf-315">下列程式碼提供如何您也可以使用 fluent API 而非屬性來指定之間的關聯性的範例`Instructor`和`OfficeAssignment`實體：</span><span class="sxs-lookup"><span data-stu-id="20adf-315">The following code provides an example of how you could have used fluent API instead of attributes to specify the relationship between the `Instructor` and `OfficeAssignment` entities:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

<span data-ttu-id="20adf-316">如需 「 fluent API 」 陳述式在幕後的執行資訊，請參閱[Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx)部落格文章。</span><span class="sxs-lookup"><span data-stu-id="20adf-316">For information about what "fluent API" statements are doing behind the scenes, see the [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog post.</span></span>

## <a name="seed-database-with-test-data"></a><span data-ttu-id="20adf-317">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-317">Seed database with test data</span></span>

<span data-ttu-id="20adf-318">中的程式碼取代*Migrations\Configuration.cs*檔案取代下列程式碼，以針對您已建立的新實體提供種子資料。</span><span class="sxs-lookup"><span data-stu-id="20adf-318">Replace the code in the *Migrations\Configuration.cs* file with the following code in order to provide seed data for the new entities you've created.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

<span data-ttu-id="20adf-319">如您所見第一個教學課程中，大部分的這段程式碼只是更新或建立新的實體物件並載入範例資料所需的測試的屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-319">As you saw in the first tutorial, most of this code simply updates or creates new entity objects and loads sample data into properties as required for testing.</span></span> <span data-ttu-id="20adf-320">不過請注意如何`Course`具有多對多關聯性的實體與`Instructor`實體，會處理：</span><span class="sxs-lookup"><span data-stu-id="20adf-320">However, notice how the `Course` entity, which has a many-to-many relationship with the `Instructor` entity, is handled:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

<span data-ttu-id="20adf-321">當您建立`Course`物件，初始化`Instructors`導覽屬性，以空的集合，使用程式碼`Instructors = new List<Instructor>()`。</span><span class="sxs-lookup"><span data-stu-id="20adf-321">When you create a `Course` object, you initialize the `Instructors` navigation property as an empty collection using the code `Instructors = new List<Instructor>()`.</span></span> <span data-ttu-id="20adf-322">這讓您能夠新增`Instructor`與此相關的實體`Course`使用`Instructors.Add`方法。</span><span class="sxs-lookup"><span data-stu-id="20adf-322">This makes it possible to add `Instructor` entities that are related to this `Course` by using the `Instructors.Add` method.</span></span> <span data-ttu-id="20adf-323">如果您未建立空的清單，您便無法將這些關聯性，因為`Instructors`屬性會是 null，而且不會有`Add`方法。</span><span class="sxs-lookup"><span data-stu-id="20adf-323">If you didn't create an empty list, you wouldn't be able to add these relationships, because the `Instructors` property would be null and wouldn't have an `Add` method.</span></span> <span data-ttu-id="20adf-324">您也可以加入清單初始化建構函式。</span><span class="sxs-lookup"><span data-stu-id="20adf-324">You could also add the list initialization to the constructor.</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="20adf-325">新增移轉</span><span class="sxs-lookup"><span data-stu-id="20adf-325">Add a migration</span></span>

<span data-ttu-id="20adf-326">在 PMC 中，輸入`add-migration`命令 (沒有`update-database`命令):</span><span class="sxs-lookup"><span data-stu-id="20adf-326">From the PMC, enter the `add-migration` command (don't do the `update-database` command yet):</span></span>

`add-Migration ComplexDataModel`

<span data-ttu-id="20adf-327">若您嘗試在這個時間點執行 `update-database` 命令，您會接收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="20adf-327">If you tried to run the `update-database` command at this point (don't do it yet), you would get the following error:</span></span>

<span data-ttu-id="20adf-328">*ALTER TABLE 陳述式與 FOREIGN KEY 條件約束 」 FK\_dbo。課程\_dbo。部門\_DepartmentID"。衝突發生在資料庫"ContosoUniversity"，資料表"dbo。部門 」，資料行 'DepartmentID'。*</span><span class="sxs-lookup"><span data-stu-id="20adf-328">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Course\_dbo.Department\_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.*</span></span>

<span data-ttu-id="20adf-329">有時當您執行使用現有的資料移轉時，您需要將 stub 資料插入資料庫中以滿足外部索引鍵條件約束，，而且這是您必須立即執行的作業。</span><span class="sxs-lookup"><span data-stu-id="20adf-329">Sometimes when you execute migrations with existing data, you need to insert stub data into the database to satisfy foreign key constraints, and that's what you have to do now.</span></span> <span data-ttu-id="20adf-330">產生的程式碼中 ComplexDataModel`Up`方法會將一個不可為 null`DepartmentID`外部索引鍵`Course`資料表。</span><span class="sxs-lookup"><span data-stu-id="20adf-330">The generated code in the ComplexDataModel `Up` method adds a non-nullable `DepartmentID` foreign key to the `Course` table.</span></span> <span data-ttu-id="20adf-331">因為已經有資料列`Course`資料表時執行的程式碼，`AddColumn`作業將會失敗，因為 SQL Server 並不知道所要放入不可為 null 的資料行的值。</span><span class="sxs-lookup"><span data-stu-id="20adf-331">Because there are already rows in the `Course` table when the code runs, the `AddColumn` operation will fail because SQL Server doesn't know what value to put in the column that can't be null.</span></span> <span data-ttu-id="20adf-332">因此必須變更為新的資料行預設值，並建立名為"Temp"作為預設部門的 stub 部門的程式碼。</span><span class="sxs-lookup"><span data-stu-id="20adf-332">Therefore have to change the code to give the new column a default value, and create a stub department named "Temp" to act as the default department.</span></span> <span data-ttu-id="20adf-333">如此一來，現有`Course`資料列將所有相關後與"Temp"部門`Up`方法執行。</span><span class="sxs-lookup"><span data-stu-id="20adf-333">As a result, existing `Course` rows will all be related to the "Temp" department after the `Up` method runs.</span></span> <span data-ttu-id="20adf-334">您可以與它們在正確的部門`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="20adf-334">You can relate them to the correct departments in the `Seed` method.</span></span>

<span data-ttu-id="20adf-335">編輯&lt;*時間戳記&gt;\_ComplexDataModel.cs*檔案，至 Course 資料表中，新增 DepartmentID 資料行的程式碼行註解，並新增下列醒目提示程式碼 （加上註解線條會也反白顯示）：</span><span class="sxs-lookup"><span data-stu-id="20adf-335">Edit the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, comment out the line of code that adds the DepartmentID column to the Course table, and add the following highlighted code (the commented line is also highlighted):</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

<span data-ttu-id="20adf-336">當`Seed`方法執行時，它會插入資料列`Department`資料表也會與現有`Course`這些新的資料列`Department`資料列。</span><span class="sxs-lookup"><span data-stu-id="20adf-336">When the `Seed` method runs, it will insert rows in the `Department` table and it will relate existing `Course` rows to those new `Department` rows.</span></span> <span data-ttu-id="20adf-337">如果您尚未新增任何課程在 UI 中，然後您不再需要"Temp"部門或預設值在`Course.DepartmentID`資料行。</span><span class="sxs-lookup"><span data-stu-id="20adf-337">If you haven't added any courses in the UI, you would then no longer need the "Temp" department or the default value on the `Course.DepartmentID` column.</span></span> <span data-ttu-id="20adf-338">若要允許，有人可能已經加入課程所使用的應用程式的可能性，也要更新`Seed`方法的程式碼，以確保所有`Course`資料列 (而不只是由先前執行插入`Seed`方法) 具有有效`DepartmentID`之前先移除預設的值從資料行值，並刪除"Temp"部門。</span><span class="sxs-lookup"><span data-stu-id="20adf-338">To allow for the possibility that someone might have added courses by using the application, you'd also want to update the `Seed` method code to ensure that all `Course` rows (not just the ones inserted by earlier runs of the `Seed` method) have valid `DepartmentID` values before you remove the default value from the column and delete the "Temp" department.</span></span>

## <a name="update-the-database"></a><span data-ttu-id="20adf-339">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-339">Update the database</span></span>

<span data-ttu-id="20adf-340">當您完成編輯之後&lt;*時間戳記&gt;\_ComplexDataModel.cs*檔案中，輸入`update-database`在 PMC 中執行移轉命令。</span><span class="sxs-lookup"><span data-stu-id="20adf-340">After you have finished editing the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, enter the `update-database` command in the PMC to execute the migration.</span></span>

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> <span data-ttu-id="20adf-341">可以移轉資料和制定的結構描述變更時，取得其他錯誤。</span><span class="sxs-lookup"><span data-stu-id="20adf-341">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="20adf-342">如果收到無法解決的移轉錯誤，您可以變更連接字串中的資料庫名稱，或刪除該資料庫。</span><span class="sxs-lookup"><span data-stu-id="20adf-342">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="20adf-343">簡單的方法是在資料庫重新命名*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="20adf-343">The simplest approach is to rename the database in *Web.config* file.</span></span> <span data-ttu-id="20adf-344">下列範例顯示名稱變更為 CU\_測試：</span><span class="sxs-lookup"><span data-stu-id="20adf-344">The following example shows the name changed to CU\_Test:</span></span>
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> <span data-ttu-id="20adf-345">使用新資料庫時，沒有資料移轉，而`update-database`命令是很有可能能順利完成。</span><span class="sxs-lookup"><span data-stu-id="20adf-345">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="20adf-346">如需有關如何刪除資料庫的指示，請參閱 <<c0> [ 如何從 Visual Studio 2012 中卸除資料庫](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="20adf-346">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span>
>
> <span data-ttu-id="20adf-347">如果失敗，您可以嘗試的另一項是將資料庫重新初始化在 PMC 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="20adf-347">If that fails, another thing you can try is re-initialize the database by entering the following command in the PMC:</span></span>
>
> `update-database -TargetMigration:0`

<span data-ttu-id="20adf-348">開啟中的資料庫**伺服器總管**當您稍早，並展開**資料表**節點以查看所有的資料表已建立的。</span><span class="sxs-lookup"><span data-stu-id="20adf-348">Open the database in **Server Explorer** as you did earlier, and expand the **Tables** node to see that all of the tables have been created.</span></span> <span data-ttu-id="20adf-349">(如果您仍有**伺服器總管**開啟從稍早的時間，再按**重新整理** 按鈕。)</span><span class="sxs-lookup"><span data-stu-id="20adf-349">(If you still have **Server Explorer** open from the earlier time, click the **Refresh** button.)</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

<span data-ttu-id="20adf-350">您未建立的模型類別`CourseInstructor`資料表。</span><span class="sxs-lookup"><span data-stu-id="20adf-350">You didn't create a model class for the `CourseInstructor` table.</span></span> <span data-ttu-id="20adf-351">如先前所述，這是一個聯結資料表之間的多對多關聯性`Instructor`和`Course`實體。</span><span class="sxs-lookup"><span data-stu-id="20adf-351">As explained earlier, this is a join table for the many-to-many relationship between the `Instructor` and `Course` entities.</span></span>

<span data-ttu-id="20adf-352">以滑鼠右鍵按一下`CourseInstructor`資料表，然後選取**顯示資料表資料**以確認它的資料中的`Instructor`實體新增至`Course.Instructors`導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="20adf-352">Right-click the `CourseInstructor` table and select **Show Table Data** to verify that it has data in it as a result of the `Instructor` entities you added to the `Course.Instructors` navigation property.</span></span>

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a><span data-ttu-id="20adf-354">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="20adf-354">Get the code</span></span>

[<span data-ttu-id="20adf-355">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="20adf-355">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="20adf-356">其他資源</span><span class="sxs-lookup"><span data-stu-id="20adf-356">Additional resources</span></span>

<span data-ttu-id="20adf-357">其他 Entity Framework 資源連結可在[ASP.NET 資料存取-建議資源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="20adf-357">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20adf-358">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20adf-358">Next steps</span></span>

<span data-ttu-id="20adf-359">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="20adf-359">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="20adf-360">自訂資料模型</span><span class="sxs-lookup"><span data-stu-id="20adf-360">Customized the data model</span></span>
> * <span data-ttu-id="20adf-361">已更新的 Student 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-361">Updated Student entity</span></span>
> * <span data-ttu-id="20adf-362">建立 Instructor 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-362">Created Instructor entity</span></span>
> * <span data-ttu-id="20adf-363">建立 OfficeAssignment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-363">Created OfficeAssignment entity</span></span>
> * <span data-ttu-id="20adf-364">修改 Course 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-364">Modified the Course entity</span></span>
> * <span data-ttu-id="20adf-365">建立 Department 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-365">Created the Department entity</span></span>
> * <span data-ttu-id="20adf-366">修改 Enrollment 實體</span><span class="sxs-lookup"><span data-stu-id="20adf-366">Modified the Enrollment entity</span></span>
> * <span data-ttu-id="20adf-367">新增的程式碼的資料庫內容</span><span class="sxs-lookup"><span data-stu-id="20adf-367">Added code to database context</span></span>
> * <span data-ttu-id="20adf-368">將測試資料植入資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-368">Seeded database with test data</span></span>
> * <span data-ttu-id="20adf-369">新增移轉</span><span class="sxs-lookup"><span data-stu-id="20adf-369">Added a migration</span></span>
> * <span data-ttu-id="20adf-370">更新資料庫</span><span class="sxs-lookup"><span data-stu-id="20adf-370">Updated the database</span></span>

<span data-ttu-id="20adf-371">請前往下一篇文章，以了解如何讀取和顯示 Entity Framework 載入到導覽屬性的相關的資料。</span><span class="sxs-lookup"><span data-stu-id="20adf-371">Advance to the next article to learn how to read and display related data that the Entity Framework loads into navigation properties.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="20adf-372">讀取相關資料</span><span class="sxs-lookup"><span data-stu-id="20adf-372">Read related data</span></span>](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
