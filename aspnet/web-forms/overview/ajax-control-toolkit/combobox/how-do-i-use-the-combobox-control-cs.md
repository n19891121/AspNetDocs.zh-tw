---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 如何使用組合盒控件? (C#) |微軟文件
author: rick-anderson
description: ComboBox 是一ASP.NET AJAX 控制項,它將TextBox的靈活性與使用者可以選擇的選項清單相結合。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543801"
---
# <a name="how-do-i-use-the-combobox-control-c"></a><span data-ttu-id="b9784-104">如何使用組合盒控件?</span><span class="sxs-lookup"><span data-stu-id="b9784-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="b9784-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="b9784-105">(C#)</span></span>

<span data-ttu-id="b9784-106">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b9784-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b9784-107">ComboBox 是一ASP.NET AJAX 控制項,它將TextBox的靈活性與使用者可以選擇的選項清單相結合。</span><span class="sxs-lookup"><span data-stu-id="b9784-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="b9784-108">本教學的目的是解釋 AJAX 控制工具組組合盒控制件。</span><span class="sxs-lookup"><span data-stu-id="b9784-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="b9784-109">組合框的工作方式類似於標準ASP.NET下拉清單控制項和文字框控制元件之間的組合。</span><span class="sxs-lookup"><span data-stu-id="b9784-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="b9784-110">您可以從預先存在的項目清單中選擇,也可以輸入新專案。</span><span class="sxs-lookup"><span data-stu-id="b9784-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="b9784-111">組合盒類似於自動完成控制器擴充器,但控制項在不同的方案中使用。</span><span class="sxs-lookup"><span data-stu-id="b9784-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="b9784-112">自動完成擴展程序查詢 Web 服務以獲取匹配的條目。</span><span class="sxs-lookup"><span data-stu-id="b9784-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="b9784-113">相反,組合框控制項使用一組項進行初始化。</span><span class="sxs-lookup"><span data-stu-id="b9784-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="b9784-114">使用 AutoComplete 擴充程式在使用大量資料(數百萬個汽車零件)時有意義,而使用 ComboBox 控制件在使用一小組數據(數十個汽車部件)時是有意義的。</span><span class="sxs-lookup"><span data-stu-id="b9784-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="b9784-115">從靜態項目清單中選擇</span><span class="sxs-lookup"><span data-stu-id="b9784-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="b9784-116">讓我們從使用組合框控件的簡單示例開始。</span><span class="sxs-lookup"><span data-stu-id="b9784-116">Let�s start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="b9784-117">假設您要在下拉清單中顯示項目的靜態清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="b9784-118">但是,您希望保留清單未完成的可能性。</span><span class="sxs-lookup"><span data-stu-id="b9784-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="b9784-119">您希望允許使用者在清單中輸入自定義值。</span><span class="sxs-lookup"><span data-stu-id="b9784-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="b9784-120">我們將創建一個新的ASP.NET Web 窗體頁,並在該頁中使用 ComboBox 控件。</span><span class="sxs-lookup"><span data-stu-id="b9784-120">We�ll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="b9784-121">將新的ASP.NET頁添加到專案中並切換到"設計"視圖。</span><span class="sxs-lookup"><span data-stu-id="b9784-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="b9784-122">如果要在頁面中使用 ComboBox 控制項,則必須向頁面添加文本管理器控制項。</span><span class="sxs-lookup"><span data-stu-id="b9784-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="b9784-123">將文稿管理器控制項從 AJAX 延伸選項卡下方拖曳到設計器表面。</span><span class="sxs-lookup"><span data-stu-id="b9784-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="b9784-124">應在頁面頂部添加腳本管理器控件;但是,在頁面頂部,應添加腳本管理器控件。可以將其添加到打開的伺服器端&lt;窗&gt;體 標記的下方。</span><span class="sxs-lookup"><span data-stu-id="b9784-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="b9784-125">接下來,將組合框控件拖到頁面上。</span><span class="sxs-lookup"><span data-stu-id="b9784-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="b9784-126">您可以在工具箱中找到與其他 AJAX 控制工具套件控制器和控制擴展器一起的 ComboBox 控制件(見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="b9784-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="b9784-127">[![建立名片的簡單表單](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="b9784-128">**圖 01**: 從工具匣中選擇群組([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="b9784-129">我們將使用組合框控件來顯示靜態選項清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-129">We�ll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="b9784-130">用戶可以從三個選項清單中為其食物選擇特定級別的辣度(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="b9784-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="b9784-131">[![從靜態項目清單中選擇](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="b9784-132">**圖 02**:從靜態項目清單中選擇([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="b9784-133">有兩種方法可以將這些選項添加到 ComboBox 控制件。</span><span class="sxs-lookup"><span data-stu-id="b9784-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="b9784-134">首先,在"設計"檢視中將滑鼠懸停在控制項上並打開專案編輯器時,請選擇"編輯選項"任務選項(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="b9784-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="b9784-135">[![編輯組合框項目](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="b9784-136">**圖 03**: 編輯組合盒項目([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="b9784-137">第二個選項是在源檢視中的開盤和關閉&lt;asp:ComboBox&gt;標記之間添加專案清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="b9784-138">清單 1 中的頁面包含包含專案清單的更新的 ComboBox。</span><span class="sxs-lookup"><span data-stu-id="b9784-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="b9784-139">**清單 1 - 靜態.aspx**</span><span class="sxs-lookup"><span data-stu-id="b9784-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

<span data-ttu-id="b9784-140">在清單 1 中開啟頁面時,您可以從組合框中選擇一個預先存在的選項。</span><span class="sxs-lookup"><span data-stu-id="b9784-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="b9784-141">換句話說,組合框的工作方式與下拉清單控件類似。</span><span class="sxs-lookup"><span data-stu-id="b9784-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="b9784-142">但是,您還可以選擇輸入不在現有清單中的新選項(例如,超級辣)。</span><span class="sxs-lookup"><span data-stu-id="b9784-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="b9784-143">因此,組合框也像文本框控件一樣工作。</span><span class="sxs-lookup"><span data-stu-id="b9784-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="b9784-144">無論您選擇預先存在的項目還是輸入自定義專案,在提交表單時,您的選擇都會顯示在標籤控制項中。</span><span class="sxs-lookup"><span data-stu-id="b9784-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="b9784-145">提交表單時,btnSubmit\_單擊處理程式將執行並更新標籤(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="b9784-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="b9784-146">[![顯示選取的項目](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="b9784-147">**圖 04**:顯示選取的項目([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="b9784-148">ComboBox 支援與提交表單後檢索選取的下拉清單控制件相同的屬性:</span><span class="sxs-lookup"><span data-stu-id="b9784-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="b9784-149">選定項目.文字 - 顯示選取的項目的文字屬性的值。</span><span class="sxs-lookup"><span data-stu-id="b9784-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="b9784-150">選定項目.值 - 顯示選取項目的值屬性的值或顯示鍵入到組合盒中的文字。</span><span class="sxs-lookup"><span data-stu-id="b9784-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="b9784-151">選取值 - 與選擇的項目相同。除非此屬性允許您指定預設(初始)選定專案。</span><span class="sxs-lookup"><span data-stu-id="b9784-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="b9784-152">如果在組合框中鍵入自定義選項,則自定義選項將分配給"選定專案.文本"和"選定專案"值屬性。</span><span class="sxs-lookup"><span data-stu-id="b9784-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="b9784-153">從資料庫中選擇項目清單</span><span class="sxs-lookup"><span data-stu-id="b9784-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="b9784-154">您可以檢索 ComboBox 從資料庫中顯示的專案清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="b9784-155">例如,您可以將組合盒綁定到 SqlDataSource 控制項、ObjectDataSource 控制項、LinqDataSource 或實體資料來源。</span><span class="sxs-lookup"><span data-stu-id="b9784-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="b9784-156">假設您要在組合盒中顯示電影清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="b9784-157">您希望從「影片」資料庫表中檢索影片清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="b9784-158">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b9784-158">Follow these steps:</span></span>

1. <span data-ttu-id="b9784-159">建立名為「電影.aspx」的頁面</span><span class="sxs-lookup"><span data-stu-id="b9784-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="b9784-160">通過將文稿管理器從工具箱中的 AJAX 擴展選項卡下拖動到頁面,將文本管理器控制項添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="b9784-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="b9784-161">通過將組合框拖到頁面上,將組合框控件添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="b9784-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="b9784-162">在"設計"檢視中,將滑鼠懸停在 ComboBox 控件上,然後選擇 **「選擇資料源**任務」選項(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="b9784-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="b9784-163">啟動數據源配置嚮導。</span><span class="sxs-lookup"><span data-stu-id="b9784-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="b9784-164">在**選擇資料來源**「步驟中,選擇」&lt;新的資料來源&gt;選項。</span><span class="sxs-lookup"><span data-stu-id="b9784-164">In the **Choose a Data Source** step, select the &lt;New data source�&gt; option.</span></span>
6. <span data-ttu-id="b9784-165">在 **「選擇資料源類型」步驟中**,選擇「資料庫」。</span><span class="sxs-lookup"><span data-stu-id="b9784-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="b9784-166">在 **「選擇數據連接**」步驟中,選擇資料庫(例如,MoviesDB.mdf)。</span><span class="sxs-lookup"><span data-stu-id="b9784-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="b9784-167">在 **「將連接字串儲存到應用程式設定檔」步驟中**,選擇儲存連接字串的選項。</span><span class="sxs-lookup"><span data-stu-id="b9784-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="b9784-168">在 **「設定選擇語句」** 步驟中,選擇「影片」資料庫表並選擇所有列。</span><span class="sxs-lookup"><span data-stu-id="b9784-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="b9784-169">在 **「測試查詢**」步驟中,按下「完成」按鈕。</span><span class="sxs-lookup"><span data-stu-id="b9784-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="b9784-170">回到 **「選擇資料來源**」步驟中,選擇要顯示的欄位的標題列和資料欄位的「Id」欄(參見圖)。</span><span class="sxs-lookup"><span data-stu-id="b9784-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="b9784-171">按下「確定」按鈕關閉精靈。</span><span class="sxs-lookup"><span data-stu-id="b9784-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="b9784-172">[![選擇資料來源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-172">[![Choosing a data source](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="b9784-173">**圖 05**: 選擇資料來源([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="b9784-174">[![選擇資料文字與值欄位](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span></span>

<span data-ttu-id="b9784-175">**圖 06**:選擇資料文字與值欄位([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span></span>

<span data-ttu-id="b9784-176">完成上述步驟后,組合Box將綁定到SqlDataSource控制項,該控制項表示「電影」資料庫表中的影片。</span><span class="sxs-lookup"><span data-stu-id="b9784-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="b9784-177">頁面的源類似於清單 2(我稍微清理了格式)。</span><span class="sxs-lookup"><span data-stu-id="b9784-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="b9784-178">**清單 2 - 電影.aspx**</span><span class="sxs-lookup"><span data-stu-id="b9784-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

<span data-ttu-id="b9784-179">請注意,ComboBox 控制件具有指向 SqlDataSource 控制件的 DataSourceID 屬性。</span><span class="sxs-lookup"><span data-stu-id="b9784-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="b9784-180">在瀏覽器中打開頁面時,將顯示資料庫中的影片清單(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="b9784-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="b9784-181">您可以透過在組合盒中鍵入影片從清單中選取影片或輸入新影片。</span><span class="sxs-lookup"><span data-stu-id="b9784-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="b9784-182">[![顯示電影清單](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span></span>

<span data-ttu-id="b9784-183">**圖 07**: 顯示電影列表([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="b9784-184">設定下拉式式</span><span class="sxs-lookup"><span data-stu-id="b9784-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="b9784-185">您可以使用組合盒下拉列表樣式屬性更改組合框的行為。</span><span class="sxs-lookup"><span data-stu-id="b9784-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="b9784-186">此屬性接受可能存在的值:</span><span class="sxs-lookup"><span data-stu-id="b9784-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="b9784-187">下拉 - (預設值) 當您按下箭頭並且可以輸入自訂值時,組合框將顯示下拉清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="b9784-188">簡單 - 組合框會自動顯示下拉清單,您可以輸入自訂值。</span><span class="sxs-lookup"><span data-stu-id="b9784-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="b9784-189">下拉清單 - 組合框的工作方式與下拉清單控制項類似。</span><span class="sxs-lookup"><span data-stu-id="b9784-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="b9784-190">下拉清單和「簡單」之間的不同是顯示項目清單時。</span><span class="sxs-lookup"><span data-stu-id="b9784-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="b9784-191">在 Simple 的情況下,當您將焦點移動到組合框時,將立即顯示清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="b9784-192">在下拉清單的情況下,必須按一下箭頭才能看到專案清單。</span><span class="sxs-lookup"><span data-stu-id="b9784-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="b9784-193">"下拉清單"值使組合盒控制項的工作方式與標準的下拉清單控制項類似。</span><span class="sxs-lookup"><span data-stu-id="b9784-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="b9784-194">然而,這裡有一個重要的區別。</span><span class="sxs-lookup"><span data-stu-id="b9784-194">However, there is an important difference here.</span></span> <span data-ttu-id="b9784-195">較舊版本的 Internet Explorer 顯示具有無限 z 索引的下拉清單控制項,因此該控制項將顯示在放置在其前面的任何控制項的前面。</span><span class="sxs-lookup"><span data-stu-id="b9784-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="b9784-196">由於組合&lt;框呈現 HTML&gt;div&lt;標籤&gt;而不是 HTML 選擇 標記,因此組合框正確尊重 z 排序。</span><span class="sxs-lookup"><span data-stu-id="b9784-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="b9784-197">設定自動完成模式</span><span class="sxs-lookup"><span data-stu-id="b9784-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="b9784-198">您可以使用 ComboBox 自動完成模式屬性來指定當有人在組合框中鍵入文本時會發生什麼情況。</span><span class="sxs-lookup"><span data-stu-id="b9784-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="b9784-199">此屬性接受以下可能的值:</span><span class="sxs-lookup"><span data-stu-id="b9784-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="b9784-200">無 - (默認值) 組合框不提供任何自動完成行為。</span><span class="sxs-lookup"><span data-stu-id="b9784-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="b9784-201">建議 - 組合框顯示清單,並突出顯示清單中的匹配項(參見圖 8)。</span><span class="sxs-lookup"><span data-stu-id="b9784-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="b9784-202">附加 - 組合框不顯示清單,它將匹配項從清單中追加到已鍵入的內容(參見圖 9)。</span><span class="sxs-lookup"><span data-stu-id="b9784-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="b9784-203">建議應用 - 組合框都會顯示清單並將匹配項從清單中追加到已鍵入的內容上(參見圖 10)。</span><span class="sxs-lookup"><span data-stu-id="b9784-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="b9784-204">[![組合盒提出建議](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span></span>

<span data-ttu-id="b9784-205">**圖 08**: 組合框提出建議([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span></span>

<span data-ttu-id="b9784-206">[![組合盒附加符合文字](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span></span>

<span data-ttu-id="b9784-207">**圖 09**: 組合盒中的文字([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span></span>

<span data-ttu-id="b9784-208">[![組合框建議與新增](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="b9784-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span></span>

<span data-ttu-id="b9784-209">**圖10**: 組合框建議與新增([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="b9784-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="b9784-210">總結</span><span class="sxs-lookup"><span data-stu-id="b9784-210">Summary</span></span>

<span data-ttu-id="b9784-211">在本教學中,您學習了如何使用 ComboBox 控件來顯示一組固定的專案。</span><span class="sxs-lookup"><span data-stu-id="b9784-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="b9784-212">我們將組合框控件綁定到靜態項集和資料庫表。</span><span class="sxs-lookup"><span data-stu-id="b9784-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="b9784-213">最後,您學習了如何通過設置其下拉風格和自動完成模式屬性來修改組合盒的行為。</span><span class="sxs-lookup"><span data-stu-id="b9784-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b9784-214">下一步</span><span class="sxs-lookup"><span data-stu-id="b9784-214">Next</span></span>](how-do-i-use-the-combobox-control-vb.md)
