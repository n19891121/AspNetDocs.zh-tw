---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: 使用資料註解驗證器 (C#) 進行驗證 |微軟文件
author: rick-anderson
description: 利用數據註釋模型綁定器在 mVC 應用程式中執行驗證ASP.NET。 瞭解如何使用不同類型的驗證器...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: 28ea52b9b412431d59d7afdd1c7cce93a50a7e2a
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542673"
---
# <a name="validation-with-the-data-annotation-validators-c"></a><span data-ttu-id="ce5bb-104">驗證與資料註解驗證器 (C#)</span><span class="sxs-lookup"><span data-stu-id="ce5bb-104">Validation with the Data Annotation Validators (C#)</span></span>

<span data-ttu-id="ce5bb-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ce5bb-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ce5bb-106">利用數據註釋模型綁定器在 mVC 應用程式中執行驗證ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="ce5bb-107">瞭解如何使用不同類型的驗證器屬性,並在 Microsoft 實體框架中使用它們。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="ce5bb-108">在本教學中,您將瞭解如何使用數據註釋驗證器在 ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="ce5bb-109">使用數據註釋驗證器的優點是,它們僅通過向類屬性添加一個或多個屬性(如"必需"或"字串長度"屬性)即可執行驗證。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="ce5bb-110">在使用數據註釋驗證器之前,必須下載數據註釋模型綁定器。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="ce5bb-111">您可以通過[按一下此處](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)從 CodePlex 網站下載數據註釋模型粘合劑範例。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="ce5bb-112">請務必瞭解,數據註釋模型綁定器不是 Microsoft ASP.NET MVC 框架的正式部分。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="ce5bb-113">儘管數據註釋模型活頁夾是由 Microsoft ASP.NET MVC 團隊創建的,但 Microsoft 不會為本教程中介紹和使用的數據註釋模型粘合劑提供官方產品支援。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="ce5bb-114">使用資料註解模型繫結器</span><span class="sxs-lookup"><span data-stu-id="ce5bb-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="ce5bb-115">為了在ASP.NET MVC 應用程式中使用數據註釋模型綁定器,首先需要添加對 Microsoft.Web.Mvc.Dataannotations.dll 程式集和 System.元件模型.Datathethe.dll 程式集的引用。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="ce5bb-116">選擇選單選項 **「專案」,新增參考**。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="ce5bb-117">接下來,按一下 **「瀏覽」** 選項卡並瀏覽到下載(並解壓縮)數據註釋模型裝訂器範例的位置(參見**圖 1)。**</span><span class="sxs-lookup"><span data-stu-id="ce5bb-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

<span data-ttu-id="ce5bb-118">**圖 1**: 新增對資料註解模型載入([按下以檢視全尺寸影像](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ce5bb-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span></span>

<span data-ttu-id="ce5bb-119">同時選擇 Microsoft.Web.Mvc.Data註解.dll 程式集和系統.元件模型.DataAnnotations.dll 程式集,然後單擊 **"確定"** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="ce5bb-120">不能使用系統.元件模型.Data註釋.dll 程式集包含在 .NET 框架服務包 1 與數據註釋模型綁定器。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="ce5bb-121">您必須使用系統版本.元件模型.Data註釋.dll 程式集包含在數據註釋模型裝訂器示例下載中。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="ce5bb-122">最後,您需要在 Global.asax 檔中註冊 DataAnnotations 模型綁定器。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="ce5bb-123">將以下代碼列加入到應用程式\_Start() 事件處理程式,\_以便應用程式 Start() 方法如下所示:</span><span class="sxs-lookup"><span data-stu-id="ce5bb-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

<span data-ttu-id="ce5bb-124">此代碼行將 ataAnnotationsModelBinder 註冊為整個ASP.NET MVC 應用程式的預設模型活頁夾。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-124">This line of code registers the ataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="ce5bb-125">使用資料註解驗證器屬性</span><span class="sxs-lookup"><span data-stu-id="ce5bb-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="ce5bb-126">使用數據註釋模型裝訂器時,可以使用驗證器屬性執行驗證。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="ce5bb-127">系統.元件模型.Data註解命名空間包括以下驗證器屬性:</span><span class="sxs-lookup"><span data-stu-id="ce5bb-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="ce5bb-128">範圍 – 使您能夠驗證屬性的值是否介於指定的值範圍之間。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="ce5bb-129">正規表示式 – 使您能夠驗證屬性的值是否與指定的正規表示式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="ce5bb-130">必需 = 使您能夠根據需要標記屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="ce5bb-131">字串長度 – 使您能夠為字串屬性指定最大長度。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="ce5bb-132">驗證 = 所有驗證器屬性的基類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ce5bb-133">如果任何標準驗證器未滿足驗證需求,則始終可以選擇通過從基本驗證屬性繼承新的驗證器屬性來創建自定義驗證器屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="ce5bb-134">**清單1**中的「產品」類說明瞭如何使用這些驗證器屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="ce5bb-135">名稱、說明和單價屬性按要求進行標記。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="ce5bb-136">Name 屬性的字串長度必須小於 10 個字元。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="ce5bb-137">最後,UnitPrice 屬性必須匹配表示貨幣金額的正則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

<span data-ttu-id="ce5bb-138">**清單1**:型號\產品.cs</span><span class="sxs-lookup"><span data-stu-id="ce5bb-138">**Listing 1**: Models\Product.cs</span></span>

<span data-ttu-id="ce5bb-139">"產品"類說明瞭如何使用一個附加屬性:顯示名稱屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="ce5bb-140">在錯誤訊息中顯示屬性時,顯示Name 屬性允許您修改屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="ce5bb-141">您可以顯示錯誤消息"需要價格",而不是顯示錯誤消息"需要價格"</span><span class="sxs-lookup"><span data-stu-id="ce5bb-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ce5bb-142">如果要完全自訂驗證器顯示的錯誤訊息,則可以將自訂錯誤訊息分配給驗證器的 ErrorMessage 屬性,如下所示:`<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="ce5bb-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="ce5bb-143">您可以將**清單 1**中的「產品」類與 清單**2**中的 Create() 控制器操作一起使用。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="ce5bb-144">當模型狀態包含任何錯誤時,此控制器操作重新顯示"創建"檢視。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

<span data-ttu-id="ce5bb-145">**清單2**:控制器\產品控制器.vb</span><span class="sxs-lookup"><span data-stu-id="ce5bb-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="ce5bb-146">最後,您可以通過右鍵單擊 Create() 操作並選擇功能表選項 **「添加檢視**」來在**清單 3**中創建檢視。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="ce5bb-147">創建以 Product 類為模型類的強類型視圖。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="ce5bb-148">從檢視內容下拉清單中**選擇"創建**"(參見**圖 2**)。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

<span data-ttu-id="ce5bb-149">**圖 2**: 新增建立檢視</span><span class="sxs-lookup"><span data-stu-id="ce5bb-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

<span data-ttu-id="ce5bb-150">**清單3**:檢視\產品\創建.aspx</span><span class="sxs-lookup"><span data-stu-id="ce5bb-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ce5bb-151">從「**新增檢視」** 選單選項產生的「創建窗體」 中移除「 Id」 欄位。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="ce5bb-152">由於 Id 欄位對應於標識列,因此您不希望允許使用者輸入此欄位的值。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="ce5bb-153">如果提交表單以創建產品,並且未輸入所需欄位的值,則將顯示**圖 3**中的驗證錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

<span data-ttu-id="ce5bb-154">**圖 3**:缺少必填欄位</span><span class="sxs-lookup"><span data-stu-id="ce5bb-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="ce5bb-155">如果輸入無效的貨幣金額,則將顯示**圖 4**中的錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

<span data-ttu-id="ce5bb-156">**圖4**:無效貨幣金額</span><span class="sxs-lookup"><span data-stu-id="ce5bb-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="ce5bb-157">將資料註解驗證器與實體框架一起使用</span><span class="sxs-lookup"><span data-stu-id="ce5bb-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="ce5bb-158">如果使用 Microsoft 實體框架生成數據模型類,則無法將驗證器屬性直接應用於類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="ce5bb-159">由於實體框架設計器生成模型類,因此下次在設計器中進行任何更改時,將對模型類所做的任何更改都將被覆蓋。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="ce5bb-160">如果要將驗證器與實體框架生成的類一起使用,則需要創建元數據類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="ce5bb-161">將驗證器應用於元數據類,而不是將驗證器應用於實際類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="ce5bb-162">例如,假設您已使用實體框架創建了 Movie 類(參見**圖 5**)。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="ce5bb-163">此外,假設您要使影片標題和導演屬性成為所需的屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="ce5bb-164">在這種情況下,您可以在**清單 4**中創建部分類和元數據類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

<span data-ttu-id="ce5bb-165">**圖 5**: 實體框架產生的影片類別</span><span class="sxs-lookup"><span data-stu-id="ce5bb-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

<span data-ttu-id="ce5bb-166">**清單4**: 模型_電影.cs</span><span class="sxs-lookup"><span data-stu-id="ce5bb-166">**Listing 4**: Models\Movie.cs</span></span>

<span data-ttu-id="ce5bb-167">**清單4**中的檔包含名為「電影」和「MovieMetaData」的兩個類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="ce5bb-168">"影片"類是部分類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-168">The Movie class is a partial class.</span></span> <span data-ttu-id="ce5bb-169">它對應於數據模型.Designer.vb 檔中包含的實體框架生成的部分類。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="ce5bb-170">目前,.NET 框架不支援部分屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="ce5bb-171">因此,無法通過將驗證器屬性應用於**清單 4**中檔中定義的 Movie 類的屬性,從而將驗證器屬性應用於 DataModel.designer.vb 檔中定義的 Movie 類的屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="ce5bb-172">請注意,影片部分類用指向 MovieMetaData 類的元數據類型屬性進行修飾。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="ce5bb-173">MovieMetaData 類包含影片類屬性的代理屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="ce5bb-174">驗證器屬性應用於 MovieMetaData 類的屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="ce5bb-175">標題、控制器和日期釋放屬性都標記為必需屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="ce5bb-176">必須為 Director 屬性分配包含少於 5 個字元的字串。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="ce5bb-177">最後,顯示Name 屬性應用於 Date 下達屬性,以顯示錯誤消息,如"需要發佈日期發佈"欄位。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="ce5bb-178">而不是錯誤"需要日期釋放欄位」。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="ce5bb-179">請注意,MovieMetaData 類中的代理屬性不需要表示與 Movie 類中的相應屬性相同的類型。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="ce5bb-180">例如,Director 屬性是 Movie 類中的字串屬性和 MovieMetaData 類中的物件屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="ce5bb-181">**圖 6**中的頁面演示了在為 Movie 屬性輸入無效值時返回的錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

<span data-ttu-id="ce5bb-182">**圖 6**: 使用驗證器與實體框架 ([按下以檢視全尺寸影像](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="ce5bb-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="ce5bb-183">總結</span><span class="sxs-lookup"><span data-stu-id="ce5bb-183">Summary</span></span>

<span data-ttu-id="ce5bb-184">在本教學中,您學習了如何使用數據註釋模型綁定器在ASP.NET MVC 應用程式中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="ce5bb-185">您學習了如何使用不同類型的驗證器屬性,如"必需"和"字串長度"屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="ce5bb-186">在使用 Microsoft 實體框架時,您還學習了如何使用這些屬性。</span><span class="sxs-lookup"><span data-stu-id="ce5bb-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ce5bb-187">[前一個](validating-with-a-service-layer-cs.md)
> [下一個](creating-model-classes-with-the-entity-framework-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ce5bb-187">[Previous](validating-with-a-service-layer-cs.md)
[Next](creating-model-classes-with-the-entity-framework-vb.md)</span></span>
