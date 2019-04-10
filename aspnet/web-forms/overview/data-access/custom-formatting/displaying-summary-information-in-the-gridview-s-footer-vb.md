---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
title: 在 GridView 的頁尾 (VB) 顯示摘要資訊 |Microsoft Docs
author: rick-anderson
description: 底部的 摘要的資料列中的報表通常顯示摘要資訊。 GridView 控制項可以包含頁尾資料列至其儲存格中，我們可以提取要求...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 41c818b7-603a-402b-8847-890a63547b6f
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 69548e637a35c4fd5d0f3356e279f1f0370fad39
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409443"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-vb"></a><span data-ttu-id="48735-104">在 GridView 的頁尾顯示摘要資訊 (VB)</span><span class="sxs-lookup"><span data-stu-id="48735-104">Displaying Summary Information in the GridView's Footer (VB)</span></span>

<span data-ttu-id="48735-105">藉由[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="48735-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="48735-106">[下載範例應用程式](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe)或[下載 PDF](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="48735-106">[Download Sample App](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe) or [Download PDF](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)</span></span>

> <span data-ttu-id="48735-107">底部的 摘要的資料列中的報表通常顯示摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="48735-107">Summary information is often displayed at the bottom of the report in a summary row.</span></span> <span data-ttu-id="48735-108">GridView 控制項可以包含頁尾資料列至其儲存格中我們以程式設計的方式可將彙總資料。</span><span class="sxs-lookup"><span data-stu-id="48735-108">The GridView control can include a footer row into whose cells we can programmatically inject aggregate data.</span></span> <span data-ttu-id="48735-109">在本教學課程中，我們會看到此頁尾資料列中顯示彙總資料的方式。</span><span class="sxs-lookup"><span data-stu-id="48735-109">In this tutorial we'll see how to display aggregate data in this footer row.</span></span>


## <a name="introduction"></a><span data-ttu-id="48735-110">簡介</span><span class="sxs-lookup"><span data-stu-id="48735-110">Introduction</span></span>

<span data-ttu-id="48735-111">除了您可以看到每個產品的價格、 庫存單位數 」、 「 單位訂單及重新排列層級上，使用者可能也會想要彙總的資訊，例如平均的價格、 庫存量，總數等等。</span><span class="sxs-lookup"><span data-stu-id="48735-111">In addition to seeing each of the products' prices, units in stock, units on order, and reorder levels, a user might also be interested in aggregate information, such as the average price, the total number of units in stock, and so on.</span></span> <span data-ttu-id="48735-112">這類摘要的資訊通常會顯示在摘要的資料列中的報表底部。</span><span class="sxs-lookup"><span data-stu-id="48735-112">Such summary information is often displayed at the bottom of the report in a summary row.</span></span> <span data-ttu-id="48735-113">GridView 控制項可以包含頁尾資料列至其儲存格中我們以程式設計的方式可將彙總資料。</span><span class="sxs-lookup"><span data-stu-id="48735-113">The GridView control can include a footer row into whose cells we can programmatically inject aggregate data.</span></span>

<span data-ttu-id="48735-114">這項工作會顯示我們三個挑戰：</span><span class="sxs-lookup"><span data-stu-id="48735-114">This task presents us with three challenges:</span></span>

1. <span data-ttu-id="48735-115">設定 GridView，以顯示其頁尾資料列</span><span class="sxs-lookup"><span data-stu-id="48735-115">Configuring the GridView to display its footer row</span></span>
2. <span data-ttu-id="48735-116">決定摘要的資料;也就是如何我們計算平均價格或總和的庫存單位數？</span><span class="sxs-lookup"><span data-stu-id="48735-116">Determining the summary data; that is, how do we compute the average price or the total of the units in stock?</span></span>
3. <span data-ttu-id="48735-117">插入頁尾資料列的適當的儲存格的摘要資料</span><span class="sxs-lookup"><span data-stu-id="48735-117">Injecting the summary data into the appropriate cells of the footer row</span></span>

<span data-ttu-id="48735-118">在本教學課程中，我們將了解如何克服這些挑戰。</span><span class="sxs-lookup"><span data-stu-id="48735-118">In this tutorial we'll see how to overcome these challenges.</span></span> <span data-ttu-id="48735-119">具體來說，我們將建立頁面，其中列出與 GridView 中顯示所選的分類的產品的下拉式清單中的類別。</span><span class="sxs-lookup"><span data-stu-id="48735-119">Specifically, we'll create a page that lists the categories in a drop-down list with the selected category's products displayed in a GridView.</span></span> <span data-ttu-id="48735-120">GridView 會包含在股票和該類別中的產品順序顯示的單位總數與平均價格的頁尾資料列。</span><span class="sxs-lookup"><span data-stu-id="48735-120">The GridView will include a footer row that shows the average price and total number of units in stock and on order for products in that category.</span></span>


[![S<span data-ttu-id="48735-121">ummary 資訊會顯示在 GridView 的頁尾資料列]</span><span class="sxs-lookup"><span data-stu-id="48735-121">ummary Information is Displayed in the GridView's Footer Row]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image1.png)

<span data-ttu-id="48735-122">**圖 1**:摘要資訊會顯示在 GridView 的頁尾資料列 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="48735-122">**Figure 1**: Summary Information is Displayed in the GridView's Footer Row ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png))</span></span>


<span data-ttu-id="48735-123">本教學課程中，使用產品的主要/詳細資料介面，其分類為建置基礎的概念稍早所述[主版/詳細篩選使用 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="48735-123">This tutorial, with its category to products master/detail interface, builds upon the concepts covered in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) tutorial.</span></span> <span data-ttu-id="48735-124">如果您還沒有使用過透過先前的教學課程，請先進行潛在這一個。</span><span class="sxs-lookup"><span data-stu-id="48735-124">If you've not yet worked through the earlier tutorial, please do so before continuing on with this one.</span></span>

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a><span data-ttu-id="48735-125">步驟 1：新增類別 DropDownList 和產品的 GridView</span><span class="sxs-lookup"><span data-stu-id="48735-125">Step 1: Adding the Categories DropDownList and Products GridView</span></span>

<span data-ttu-id="48735-126">之前有關自行使用 GridView 的頁尾中加入的摘要資訊，讓我們第一次只要建置主版/詳細報告。</span><span class="sxs-lookup"><span data-stu-id="48735-126">Before concerning ourselves with adding summary information to the GridView's footer, let's first simply build the master/detail report.</span></span> <span data-ttu-id="48735-127">當我們完成第一個步驟之後時，我們將探討如何將加入摘要資料。</span><span class="sxs-lookup"><span data-stu-id="48735-127">Once we've completed this first step, we'll look at how to include summary data.</span></span>

<span data-ttu-id="48735-128">首先開啟`SummaryDataInFooter.aspx`頁面中`CustomFormatting`資料夾。</span><span class="sxs-lookup"><span data-stu-id="48735-128">Start by opening the `SummaryDataInFooter.aspx` page in the `CustomFormatting` folder.</span></span> <span data-ttu-id="48735-129">新增 DropDownList 控制項並設定其`ID`至`Categories`。</span><span class="sxs-lookup"><span data-stu-id="48735-129">Add a DropDownList control and set its `ID` to `Categories`.</span></span> <span data-ttu-id="48735-130">接下來，按一下 從 DropDownList 的智慧標籤的 選擇資料來源 連結，並選擇新增名為新 ObjectDataSource`CategoriesDataSource`叫用`CategoriesBLL`類別的`GetCategories()`方法。</span><span class="sxs-lookup"><span data-stu-id="48735-130">Next, click on the Choose Data Source link from the DropDownList's smart tag and opt to add a new ObjectDataSource named `CategoriesDataSource` that invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span>


[![A<span data-ttu-id="48735-131">dd 新 ObjectDataSource 名為 CategoriesDataSource]</span><span class="sxs-lookup"><span data-stu-id="48735-131">dd a New ObjectDataSource Named CategoriesDataSource]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image4.png)

<span data-ttu-id="48735-132">**圖 2**:新增新的 ObjectDataSource 名為`CategoriesDataSource`([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="48735-132">**Figure 2**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png))</span></span>


[![H<span data-ttu-id="48735-133">ave ObjectDataSource 會叫用 CategoriesBLL 類別的 GetCategories() 方法]</span><span class="sxs-lookup"><span data-stu-id="48735-133">ave the ObjectDataSource Invoke the CategoriesBLL Class's GetCategories() Method]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image7.png)

<span data-ttu-id="48735-134">**圖 3**:有 ObjectDataSource 叫用`CategoriesBLL`類別的`GetCategories()`方法 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="48735-134">**Figure 3**: Have the ObjectDataSource Invoke the `CategoriesBLL` Class's `GetCategories()` Method ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))</span></span>


<span data-ttu-id="48735-135">之後設定 ObjectDataSource，精靈會傳回我們 DropDownList 的資料來源組態精靈 」，我們要指定哪些資料欄位值應該會顯示，而且其中一個應該對應至 DropDownList 值的`ListItem` s。</span><span class="sxs-lookup"><span data-stu-id="48735-135">After configuring the ObjectDataSource, the wizard returns us to the DropDownList's Data Source Configuration wizard from which we need to specify what data field value should be displayed and which one should correspond to the value of the DropDownList's `ListItem` s.</span></span> <span data-ttu-id="48735-136">已`CategoryName`顯示的欄位，並使用`CategoryID`做為值。</span><span class="sxs-lookup"><span data-stu-id="48735-136">Have the `CategoryName` field displayed and use the `CategoryID` as the value.</span></span>


[![U<span data-ttu-id="48735-137">se CategoryName 和 CategoryID 視欄位的文字和值 ListItems，分別]</span><span class="sxs-lookup"><span data-stu-id="48735-137">se the CategoryName and CategoryID Fields as the Text and Value for the ListItems, Respectively]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image10.png)

<span data-ttu-id="48735-138">**圖 4**:使用`CategoryName`及`CategoryID`視欄位`Text`並`Value`如`ListItem`s，分別 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="48735-138">**Figure 4**: Use the `CategoryName` and `CategoryID` Fields as the `Text` and `Value` for the `ListItem` s, Respectively ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png))</span></span>


<span data-ttu-id="48735-139">現在我們有 DropDownList (`Categories`)，在系統中列出的類別。</span><span class="sxs-lookup"><span data-stu-id="48735-139">At this point we have a DropDownList (`Categories`) that lists the categories in the system.</span></span> <span data-ttu-id="48735-140">我們現在需要新增的 GridView 會列出這些屬於所選分類的產品。</span><span class="sxs-lookup"><span data-stu-id="48735-140">We now need to add a GridView that lists those products that belong to the selected category.</span></span> <span data-ttu-id="48735-141">這樣做，不過，先花點時間檢查 DropDownList 的智慧標籤啟用 AutoPostBack 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="48735-141">Before we do, though, take a moment to check the Enable AutoPostBack checkbox in the DropDownList's smart tag.</span></span> <span data-ttu-id="48735-142">中所述*主版/詳細篩選使用 DropDownList*教學課程中，藉由設定 DropDownList`AutoPostBack`屬性設`True`頁面將會公佈回的每當 DropDownList 值變更時。</span><span class="sxs-lookup"><span data-stu-id="48735-142">As discussed in the *Master/Detail Filtering With a DropDownList* tutorial, by setting the DropDownList's `AutoPostBack` property to `True` the page will be posted back each time the DropDownList value is changed.</span></span> <span data-ttu-id="48735-143">這會導致重新整理，GridView 顯示這些產品的新選取的分類。</span><span class="sxs-lookup"><span data-stu-id="48735-143">This will cause the GridView to be refreshed, showing those products for the newly selected category.</span></span> <span data-ttu-id="48735-144">如果`AutoPostBack`屬性設定為`False`（預設值），變更類別目錄不會造成回傳並不會更新列出的產品。</span><span class="sxs-lookup"><span data-stu-id="48735-144">If the `AutoPostBack` property is set to `False` (the default), changing the category won't cause a postback and therefore won't update the listed products.</span></span>


[![C<span data-ttu-id="48735-145">h DropDownList 的智慧標籤中的啟用 AutoPostBack 核取]</span><span class="sxs-lookup"><span data-stu-id="48735-145">heck the Enable AutoPostBack Checkbox in the DropDownList's Smart Tag]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image13.png)

<span data-ttu-id="48735-146">**圖 5**:核取方塊啟用 AutoPostBack DropDownList 的智慧標籤中 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="48735-146">**Figure 5**: Check the Enable AutoPostBack Checkbox in the DropDownList's Smart Tag ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png))</span></span>


<span data-ttu-id="48735-147">將 GridView 控制項加入頁面，以顯示所選分類的產品。</span><span class="sxs-lookup"><span data-stu-id="48735-147">Add a GridView control to the page in order to display the products for the selected category.</span></span> <span data-ttu-id="48735-148">設定 GridView`ID`要`ProductsInCategory`並將它繫結至名為新 ObjectDataSource `ProductsInCategoryDataSource`。</span><span class="sxs-lookup"><span data-stu-id="48735-148">Set the GridView's `ID` to `ProductsInCategory` and bind it to a new ObjectDataSource named `ProductsInCategoryDataSource`.</span></span>


[![A<span data-ttu-id="48735-149">dd 新 ObjectDataSource 名為 ProductsInCategoryDataSource]</span><span class="sxs-lookup"><span data-stu-id="48735-149">dd a New ObjectDataSource Named ProductsInCategoryDataSource]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image16.png)

<span data-ttu-id="48735-150">**圖 6**:新增新的 ObjectDataSource 名為`ProductsInCategoryDataSource`([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="48735-150">**Figure 6**: Add a New ObjectDataSource Named `ProductsInCategoryDataSource` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png))</span></span>


<span data-ttu-id="48735-151">因此，它會叫用設定 ObjectDataSource`ProductsBLL`類別的`GetProductsByCategoryID(categoryID)`方法。</span><span class="sxs-lookup"><span data-stu-id="48735-151">Configure the ObjectDataSource so that it invokes the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span>


[![H<span data-ttu-id="48735-152">ObjectDataSource Invoke GetProductsByCategoryID(categoryID) 方法 [ave]</span><span class="sxs-lookup"><span data-stu-id="48735-152">ave the ObjectDataSource Invoke the GetProductsByCategoryID(categoryID) Method]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image19.png)

<span data-ttu-id="48735-153">**圖 7**:有 ObjectDataSource 叫用`GetProductsByCategoryID(categoryID)`方法 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="48735-153">**Figure 7**: Have the ObjectDataSource Invoke the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png))</span></span>


<span data-ttu-id="48735-154">因為`GetProductsByCategoryID(categoryID)`方法接受一個輸入參數，在精靈的最後一個步驟中，我們可以指定參數值的來源。</span><span class="sxs-lookup"><span data-stu-id="48735-154">Since the `GetProductsByCategoryID(categoryID)` method takes in an input parameter, in the final step of the wizard we can specify the source of the parameter value.</span></span> <span data-ttu-id="48735-155">若要顯示這些產品，從選取的類別，具有 取自參數`Categories`DropDownList。</span><span class="sxs-lookup"><span data-stu-id="48735-155">In order to display those products from the selected category, have the parameter pulled from the `Categories` DropDownList.</span></span>


[![G<span data-ttu-id="48735-156">et categoryID 參數值，從選取類別 DropDownList]</span><span class="sxs-lookup"><span data-stu-id="48735-156">et the categoryID Parameter Value from the Selected Categories DropDownList]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image22.png)

<span data-ttu-id="48735-157">**圖 8**:取得*`categoryID`* 從 選取類別 DropDownList 的參數值 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="48735-157">**Figure 8**: Get the *`categoryID`* Parameter Value from the Selected Categories DropDownList ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))</span></span>


<span data-ttu-id="48735-158">完成精靈之後 GridView 將會有 BoundField 每個產品的屬性。</span><span class="sxs-lookup"><span data-stu-id="48735-158">After completing the wizard the GridView will have a BoundField for each of the product properties.</span></span> <span data-ttu-id="48735-159">讓我們清除這些 BoundFields 使得只有`ProductName`， `UnitPrice`， `UnitsInStock`，和`UnitsOnOrder`BoundFields 會顯示。</span><span class="sxs-lookup"><span data-stu-id="48735-159">Let's clean up these BoundFields so that only the `ProductName`, `UnitPrice`, `UnitsInStock`, and `UnitsOnOrder` BoundFields are displayed.</span></span> <span data-ttu-id="48735-160">歡迎您將任何欄位層級設定新增至其餘 BoundFields (格式化等`UnitPrice`為貨幣)。</span><span class="sxs-lookup"><span data-stu-id="48735-160">Feel free to add any field-level settings to the remaining BoundFields (such as formatting the `UnitPrice` as a currency).</span></span> <span data-ttu-id="48735-161">進行這些變更之後，GridView 的宣告式標記看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="48735-161">After making these changes, the GridView's declarative markup should look similar to the following:</span></span>


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample1.aspx)]

<span data-ttu-id="48735-162">此時，我們會有完整的主要/詳細資料報表，顯示名稱、 單位價格、 庫存量和單位，屬於所選分類這些產品的訂購。</span><span class="sxs-lookup"><span data-stu-id="48735-162">At this point we have a fully functioning master/detail report that shows the name, unit price, units in stock, and units on order for those products that belong to the selected category.</span></span>


[![G<span data-ttu-id="48735-163">et categoryID 參數值，從選取類別 DropDownList]</span><span class="sxs-lookup"><span data-stu-id="48735-163">et the categoryID Parameter Value from the Selected Categories DropDownList]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image25.png)

<span data-ttu-id="48735-164">**圖 9**:取得*`categoryID`* 從 選取類別 DropDownList 的參數值 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="48735-164">**Figure 9**: Get the *`categoryID`* Parameter Value from the Selected Categories DropDownList ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))</span></span>


## <a name="step-2-displaying-a-footer-in-the-gridview"></a><span data-ttu-id="48735-165">步驟 2：在 GridView 中顯示頁尾</span><span class="sxs-lookup"><span data-stu-id="48735-165">Step 2: Displaying a Footer in the GridView</span></span>

<span data-ttu-id="48735-166">GridView 控制項可以顯示頁首和頁尾資料列。</span><span class="sxs-lookup"><span data-stu-id="48735-166">The GridView control can display both a header and footer row.</span></span> <span data-ttu-id="48735-167">這些資料列會顯示依據的值`ShowHeader`並`ShowFooter`屬性，分別使用`ShowHeader`預設為`True`並`ShowFooter`來`False`。</span><span class="sxs-lookup"><span data-stu-id="48735-167">These rows are displayed depending on the values of the `ShowHeader` and `ShowFooter` properties, respectively, with `ShowHeader` defaulting to `True` and `ShowFooter` to `False`.</span></span> <span data-ttu-id="48735-168">若要直接包含在 GridView 的頁尾設定其`ShowFooter`屬性設`True`。</span><span class="sxs-lookup"><span data-stu-id="48735-168">To include a footer in the GridView simply set its `ShowFooter` property to `True`.</span></span>


[![S<span data-ttu-id="48735-169">et GridView 的 ShowFooter 屬性設為 True]</span><span class="sxs-lookup"><span data-stu-id="48735-169">et the GridView's ShowFooter Property to True]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image28.png)

<span data-ttu-id="48735-170">**圖 10**:設定 GridView`ShowFooter`屬性，以`True`([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="48735-170">**Figure 10**: Set the GridView's `ShowFooter` Property to `True` ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png))</span></span>


<span data-ttu-id="48735-171">頁尾資料列具有每個子 GridView; 內所定義之欄位的資料格不過，這些資料格預設為空白。</span><span class="sxs-lookup"><span data-stu-id="48735-171">The footer row has a cell for each of the fields defined in the GridView; however, these cells are empty by default.</span></span> <span data-ttu-id="48735-172">請花一點時間瀏覽器中檢視進度。</span><span class="sxs-lookup"><span data-stu-id="48735-172">Take a moment to view our progress in a browser.</span></span> <span data-ttu-id="48735-173">具有`ShowFooter`內容現在設定為`True`，GridView 包含空的頁尾資料列。</span><span class="sxs-lookup"><span data-stu-id="48735-173">With the `ShowFooter` property now set to `True`, the GridView includes an empty footer row.</span></span>


[![T<span data-ttu-id="48735-174">現在，他的 GridView 會包含頁尾資料列]</span><span class="sxs-lookup"><span data-stu-id="48735-174">he GridView Now Includes a Footer Row]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image31.png)

<span data-ttu-id="48735-175">**圖 11**:現在包含 GridView 的頁尾資料列 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="48735-175">**Figure 11**: The GridView Now Includes a Footer Row ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png))</span></span>


<span data-ttu-id="48735-176">[圖 11] 中的頁尾資料列不脫穎而出，因為它具有白色背景。</span><span class="sxs-lookup"><span data-stu-id="48735-176">The footer row in Figure 11 doesn't stand out, as it has a white background.</span></span> <span data-ttu-id="48735-177">讓我們來建立`FooterStyle`CSS 類別`Styles.css`指定為深紅色背景，然後設定`GridView.skin`面板中的檔案`DataWebControls`GridView 的單位為這個 CSS 類別的佈景主題`FooterStyle`的`CssClass`屬性。</span><span class="sxs-lookup"><span data-stu-id="48735-177">Let's create a `FooterStyle` CSS class in `Styles.css` that specifies a dark red background and then configure the `GridView.skin` Skin file in the `DataWebControls` Theme to assign this CSS class to the GridView's `FooterStyle`'s `CssClass` property.</span></span> <span data-ttu-id="48735-178">如果您要溫習面板和佈景主題，請參閱上一步[顯示的資料與 ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="48735-178">If you need to brush up on Skins and Themes, refer back to the [Displaying Data With the ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) tutorial.</span></span>

<span data-ttu-id="48735-179">新增下列 CSS 類別開始`Styles.css`:</span><span class="sxs-lookup"><span data-stu-id="48735-179">Start by adding the following CSS class to `Styles.css`:</span></span>


[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample2.css)]

<span data-ttu-id="48735-180">`FooterStyle` CSS 類別很類似，在樣式`HeaderStyle`類別，雖然`HeaderStyle`的背景色彩較暗的微妙影響，且它的文字會顯示以粗體字。</span><span class="sxs-lookup"><span data-stu-id="48735-180">The `FooterStyle` CSS class is similar in style to the `HeaderStyle` class, although the `HeaderStyle`'s background color is subtlety darker and its text is displayed in a bold font.</span></span> <span data-ttu-id="48735-181">此外，在頁尾中的文字會靠右對齊而標頭的文字置中。</span><span class="sxs-lookup"><span data-stu-id="48735-181">Furthermore, the text in the footer is right-aligned whereas the header's text is centered.</span></span>

<span data-ttu-id="48735-182">接下來，若要建立這個 CSS 類別的關聯與每個 GridView 的頁尾，開啟`GridView.skin`檔案中`DataWebControls`佈景主題和 set`FooterStyle`的`CssClass`屬性。</span><span class="sxs-lookup"><span data-stu-id="48735-182">Next, to associate this CSS class with every GridView's footer, open the `GridView.skin` file in the `DataWebControls` Theme and set the `FooterStyle`'s `CssClass` property.</span></span> <span data-ttu-id="48735-183">在此新增後檔案的標記應該看起來像：</span><span class="sxs-lookup"><span data-stu-id="48735-183">After this addition the file's markup should look like:</span></span>


[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample3.aspx)]

<span data-ttu-id="48735-184">這項變更如螢幕擷取畫面如下所示，讓頁尾清楚地凸顯更多。</span><span class="sxs-lookup"><span data-stu-id="48735-184">As the screen shot below shows, this change makes the footer stand out more clearly.</span></span>


[![T<span data-ttu-id="48735-185">他 GridView 的頁尾資料列現在有紅的背景色彩]</span><span class="sxs-lookup"><span data-stu-id="48735-185">he GridView's Footer Row Now Has a Reddish Background Color]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image34.png)

<span data-ttu-id="48735-186">**圖 12**:GridView 的頁尾資料列現在有紅的背景色彩 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="48735-186">**Figure 12**: The GridView's Footer Row Now Has a Reddish Background Color ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png))</span></span>


## <a name="step-3-computing-the-summary-data"></a><span data-ttu-id="48735-187">步驟 3：計算摘要資料</span><span class="sxs-lookup"><span data-stu-id="48735-187">Step 3: Computing the Summary Data</span></span>

<span data-ttu-id="48735-188">使用 GridView 的頁尾中顯示，接下來我們面臨的挑戰是如何計算摘要資料。</span><span class="sxs-lookup"><span data-stu-id="48735-188">With the GridView's footer displayed, the next challenge facing us is how to compute the summary data.</span></span> <span data-ttu-id="48735-189">有兩種方式來計算此彙總的資訊：</span><span class="sxs-lookup"><span data-stu-id="48735-189">There are two ways to compute this aggregate information:</span></span>

1. <span data-ttu-id="48735-190">透過 SQL 查詢中，我們可以發出額外的查詢資料庫以計算特定類別的摘要資料。</span><span class="sxs-lookup"><span data-stu-id="48735-190">Through a SQL query we could issue an additional query to the database to compute the summary data for a particular category.</span></span> <span data-ttu-id="48735-191">SQL 包含數個彙總函式，連同`GROUP BY`子句來指定哪些資料應該彙總的資料。</span><span class="sxs-lookup"><span data-stu-id="48735-191">SQL includes a number of aggregate functions along with a `GROUP BY` clause to specify the data over which the data should be summarized.</span></span> <span data-ttu-id="48735-192">下列 SQL 查詢會回復所需的資訊：</span><span class="sxs-lookup"><span data-stu-id="48735-192">The following SQL query would bring back the needed information:</span></span>  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample4.sql)]

    <span data-ttu-id="48735-193">當然您不想要發出這項查詢，直接從`SummaryDataInFooter.aspx`頁面上，而是藉由建立中的方法`ProductsTableAdapter`而`ProductsBLL`。</span><span class="sxs-lookup"><span data-stu-id="48735-193">Of course you wouldn't want to issue this query directly from the `SummaryDataInFooter.aspx` page, but rather by creating a method in the `ProductsTableAdapter` and the `ProductsBLL`.</span></span>
2. <span data-ttu-id="48735-194">計算這項資訊，因為它正在加入至 GridView 中所述[自訂格式設定基礎時的資料](custom-formatting-based-upon-data-cs.md)教學課程中，GridView 的`RowDataBound`事件處理常式，就會引發一次每個資料列新增至後 GridView 其已資料繫結。</span><span class="sxs-lookup"><span data-stu-id="48735-194">Compute this information as it's being added to the GridView as discussed in [Custom Formatting Based Upon Data](custom-formatting-based-upon-data-cs.md) tutorial, the GridView's `RowDataBound` event handler fires once for each row being added to the GridView after its been databound.</span></span> <span data-ttu-id="48735-195">藉由建立此事件的事件處理常式中，我們可以把執行我們想要的值的總計彙總。</span><span class="sxs-lookup"><span data-stu-id="48735-195">By creating an event handler for this event we can keep a running total of the values we want to aggregate.</span></span> <span data-ttu-id="48735-196">最後一個之後的資料列已經繫結至 GridView，我們有總計和計算平均值時，所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="48735-196">After the last data row has been bound to the GridView we have the totals and the information needed to compute the average.</span></span>

<span data-ttu-id="48735-197">我通常採用第二種方法，因為它會將某趟車程支付儲存至資料庫，以及資料存取層和商務邏輯層中實作 「 摘要 」 功能所需的心力，但兩種方法即已足夠。</span><span class="sxs-lookup"><span data-stu-id="48735-197">I typically employ the second approach as it saves a trip to the database and the effort needed to implement the summary functionality in the Data Access Layer and Business Logic Layer, but either approach would suffice.</span></span> <span data-ttu-id="48735-198">本教學課程中讓我們使用第二個選項，並累計總數的使用追蹤的`RowDataBound`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="48735-198">For this tutorial let's use the second option and keep track of the running total using the `RowDataBound` event handler.</span></span>

<span data-ttu-id="48735-199">建立`RowDataBound`事件處理常式，方法是將在設計工具中選取 GridView 中，按一下閃電圖示從 [屬性] 視窗中，按兩下 gridview`RowDataBound`事件。</span><span class="sxs-lookup"><span data-stu-id="48735-199">Create a `RowDataBound` event handler for the GridView by selecting the GridView in the Designer, clicking the lightning bolt icon from the Properties window, and double-clicking the `RowDataBound` event.</span></span> <span data-ttu-id="48735-200">或者，您可以從 ASP.NET 程式碼後置類別檔案頂端的下拉式清單選取 GridView 以及其 RowDataBound 事件。</span><span class="sxs-lookup"><span data-stu-id="48735-200">Alternatively, you can select the GridView and its RowDataBound event from the drop-down lists at the top of the ASP.NET code-behind class file.</span></span> <span data-ttu-id="48735-201">這會建立名為新的事件處理常式`ProductsInCategory_RowDataBound`在`SummaryDataInFooter.aspx`頁面的程式碼後置類別。</span><span class="sxs-lookup"><span data-stu-id="48735-201">This will create a new event handler named `ProductsInCategory_RowDataBound` in the `SummaryDataInFooter.aspx` page's code-behind class.</span></span>


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample5.vb)]

<span data-ttu-id="48735-202">為了維護執行總數中，我們必須定義變數超出範圍的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="48735-202">In order to maintain a running total we need to define variables outside of the scope of the event handler.</span></span> <span data-ttu-id="48735-203">建立下列四個頁面層級變數：</span><span class="sxs-lookup"><span data-stu-id="48735-203">Create the following four page-level variables:</span></span>

- `_totalUnitPrice`<span data-ttu-id="48735-204">型別</span><span class="sxs-lookup"><span data-stu-id="48735-204">, of type</span></span> `Decimal`
- `_totalNonNullUnitPriceCount`<span data-ttu-id="48735-205">型別</span><span class="sxs-lookup"><span data-stu-id="48735-205">, of type</span></span> `Integer`
- `_totalUnitsInStock`<span data-ttu-id="48735-206">型別</span><span class="sxs-lookup"><span data-stu-id="48735-206">, of type</span></span> `Integer`
- `_totalUnitsOnOrder`<span data-ttu-id="48735-207">型別</span><span class="sxs-lookup"><span data-stu-id="48735-207">, of type</span></span> `Integer`

<span data-ttu-id="48735-208">接下來，撰寫程式碼中遇到的每個資料列的遞增這三個變數`RowDataBound`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="48735-208">Next, write the code to increment these three variables for each data row encountered in the `RowDataBound` event handler.</span></span>


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample6.vb)]

<span data-ttu-id="48735-209">`RowDataBound`確保我們要處理的 DataRow 的事件處理常式會啟動。</span><span class="sxs-lookup"><span data-stu-id="48735-209">The `RowDataBound` event handler starts by ensuring that we're dealing with a DataRow.</span></span> <span data-ttu-id="48735-210">一旦已建立的`Northwind.ProductsRow`只是繫結至執行個體`GridViewRow`物件中`e.Row`儲存在變數`product`。</span><span class="sxs-lookup"><span data-stu-id="48735-210">Once that's been established, the `Northwind.ProductsRow` instance that was just bound to the `GridViewRow` object in `e.Row` is stored in the variable `product`.</span></span> <span data-ttu-id="48735-211">接下來，執行的總變數目前的產品對應的值以遞增 (假設它們不包含資料庫`NULL`值)。</span><span class="sxs-lookup"><span data-stu-id="48735-211">Next, running total variables are incremented by the current product's corresponding values (assuming that they don't contain a database `NULL` value).</span></span> <span data-ttu-id="48735-212">我們持續追蹤的這兩個執行`UnitPrice`總計和非數字`NULL``UnitPrice`記錄因為平均的價格是這兩個數字的商數。</span><span class="sxs-lookup"><span data-stu-id="48735-212">We keep track of both the running `UnitPrice` total and the number of non-`NULL` `UnitPrice` records because the average price is the quotient of these two numbers.</span></span>

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a><span data-ttu-id="48735-213">步驟 4：在頁尾顯示摘要資料</span><span class="sxs-lookup"><span data-stu-id="48735-213">Step 4: Displaying the Summary Data in the Footer</span></span>

<span data-ttu-id="48735-214">總計的摘要資料，最後一個步驟是在 GridView 的頁尾資料列中顯示它。</span><span class="sxs-lookup"><span data-stu-id="48735-214">With the summary data totaled, the last step is to display it in the GridView's footer row.</span></span> <span data-ttu-id="48735-215">這項工作，也可完成以程式設計方式透過`RowDataBound`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="48735-215">This task, too, can be accomplished programmatically through the `RowDataBound` event handler.</span></span> <span data-ttu-id="48735-216">請記得，`RowDataBound`針對觸發的事件處理常式*每個*繫結至 GridView，包括頁尾資料列的資料列。</span><span class="sxs-lookup"><span data-stu-id="48735-216">Recall that the `RowDataBound` event handler fires for *every* row that's bound to the GridView, including the footer row.</span></span> <span data-ttu-id="48735-217">因此，我們可以加強我們的事件處理常式，來顯示頁尾資料列，使用下列程式碼中的資料：</span><span class="sxs-lookup"><span data-stu-id="48735-217">Therefore, we can augment our event handler to display the data in the footer row using the following code:</span></span>


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample7.vb)]

<span data-ttu-id="48735-218">因為頁尾資料列加入至 GridView 之後新增所有的資料列之後，我們可以確信時我們已準備好可以顯示在頁尾中的累計總數的計算會完成的摘要資料。</span><span class="sxs-lookup"><span data-stu-id="48735-218">Since the footer row is added to the GridView after all of the data rows have been added, we can be confident that by the time we're ready to display the summary data in the footer the running total calculations will have completed.</span></span> <span data-ttu-id="48735-219">最後一個步驟中，則，是在頁尾中的資料格中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="48735-219">The last step, then, is to set these values in the footer's cells.</span></span>

<span data-ttu-id="48735-220">若要在特定的頁尾資料格中顯示文字，請使用`e.Row.Cells(index).Text = value`，其中`Cells`編製索引從 0 開始。</span><span class="sxs-lookup"><span data-stu-id="48735-220">To display text in a particular footer cell, use `e.Row.Cells(index).Text = value`, where the `Cells` indexing starts at 0.</span></span> <span data-ttu-id="48735-221">下列程式碼計算平均價格 （總計除以的數字的產品的價格），並顯示它的單位總數以及股票圖和 GridView 的頁尾適當儲存格中的訂購量。</span><span class="sxs-lookup"><span data-stu-id="48735-221">The following code computes the average price (the total price divided by the number of products) and displays it along with the total number of units in stock and units on order in the appropriate footer cells of the GridView.</span></span>


[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample8.vb)]

<span data-ttu-id="48735-222">已加入此程式碼之後，圖 13 顯示的報表。</span><span class="sxs-lookup"><span data-stu-id="48735-222">Figure 13 shows the report after this code has been added.</span></span> <span data-ttu-id="48735-223">請注意如何`ToString("c")`平均價格的摘要資訊格式化貨幣等。</span><span class="sxs-lookup"><span data-stu-id="48735-223">Note how the `ToString("c")` causes the average price summary information to be formatted like a currency.</span></span>


[![T<span data-ttu-id="48735-224">他 GridView 的頁尾資料列現在有紅的背景色彩]</span><span class="sxs-lookup"><span data-stu-id="48735-224">he GridView's Footer Row Now Has a Reddish Background Color]</span></span>(displaying-summary-information-in-the-gridview-s-footer-vb/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image37.png)

<span data-ttu-id="48735-225">**圖 13**:GridView 的頁尾資料列現在有紅的背景色彩 ([按一下以檢視完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png))</span><span class="sxs-lookup"><span data-stu-id="48735-225">**Figure 13**: The GridView's Footer Row Now Has a Reddish Background Color ([Click to view full-size image](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png))</span></span>


## <a name="summary"></a><span data-ttu-id="48735-226">總結</span><span class="sxs-lookup"><span data-stu-id="48735-226">Summary</span></span>

<span data-ttu-id="48735-227">顯示摘要資料是報表的一般需求，和 GridView 控制項可讓您輕鬆地在其頁尾資料列中包含這類資訊。</span><span class="sxs-lookup"><span data-stu-id="48735-227">Displaying summary data is a common report requirement, and the GridView control makes it easy to include such information in its footer row.</span></span> <span data-ttu-id="48735-228">顯示頁尾資料列時 GridView`ShowFooter`屬性設定為`True`可以在設定以程式設計方式透過其儲存格的文字和`RowDataBound`事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="48735-228">The footer row is displayed when the GridView's `ShowFooter` property is set to `True` and can have the text in its cells set programmatically through the `RowDataBound` event handler.</span></span> <span data-ttu-id="48735-229">計算摘要資料是可重新查詢資料庫，或使用 ASP.NET 網頁的程式碼後置類別中的程式碼，以程式設計方式計算摘要資料。</span><span class="sxs-lookup"><span data-stu-id="48735-229">Computing the summary data can either be done by re-querying the database or by using code in the ASP.NET page's code-behind class to programmatically compute the summary data.</span></span>

<span data-ttu-id="48735-230">本教學課程結束時，我們檢查與 GridView、 DetailsView 和 FormView 控制項的自訂格式。</span><span class="sxs-lookup"><span data-stu-id="48735-230">This tutorial concludes our examination of custom formatting with the GridView, DetailsView, and FormView controls.</span></span> <span data-ttu-id="48735-231">我們的下一個教學課程一開始我們探勘的插入、 更新和刪除使用這些相同的控制項的資料。</span><span class="sxs-lookup"><span data-stu-id="48735-231">Our next tutorial kicks off our exploration of inserting, updating, and deleting data using these same controls.</span></span>

<span data-ttu-id="48735-232">快樂地寫程式 ！</span><span class="sxs-lookup"><span data-stu-id="48735-232">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="48735-233">關於作者</span><span class="sxs-lookup"><span data-stu-id="48735-233">About the Author</span></span>

<span data-ttu-id="48735-234">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的七個 ASP 書籍和的創辦人[4GuysFromRolla.com](http://www.4guysfromrolla.com)，自 1998 年從事 Microsoft Web 技術工作。</span><span class="sxs-lookup"><span data-stu-id="48735-234">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="48735-235">Scott 會擔任獨立的顧問、 培訓講師和作家。</span><span class="sxs-lookup"><span data-stu-id="48735-235">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="48735-236">他最新的著作是[ *Sams 教導您自己 ASP.NET 2.0 在 24 小時內*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。</span><span class="sxs-lookup"><span data-stu-id="48735-236">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="48735-237">他可以在觸達[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="48735-237">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="48735-238">或透過他的部落格，這位於 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)。</span><span class="sxs-lookup"><span data-stu-id="48735-238">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="48735-239">上一步</span><span class="sxs-lookup"><span data-stu-id="48735-239">Previous</span></span>](using-the-formview-s-templates-vb.md)
