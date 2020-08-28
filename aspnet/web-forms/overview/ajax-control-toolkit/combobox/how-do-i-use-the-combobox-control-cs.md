---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: '如何? 使用 ComboBox 控制項？  (C # ) |Microsoft Docs'
author: rick-anderson
description: ComboBox 是 ASP.NET 的 AJAX 控制項，結合 TextBox 的彈性與使用者可以選擇的選項清單。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 035bcb2fb6cce246b904c295aba15efd17c2c232
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045061"
---
# <a name="how-do-i-use-the-combobox-control-c"></a><span data-ttu-id="f9124-104">如何? 使用 ComboBox 控制項？</span><span class="sxs-lookup"><span data-stu-id="f9124-104">How do I use the ComboBox Control?</span></span> <span data-ttu-id="f9124-105">(C#)</span><span class="sxs-lookup"><span data-stu-id="f9124-105">(C#)</span></span>

<span data-ttu-id="f9124-106">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f9124-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="f9124-107">ComboBox 是 ASP.NET 的 AJAX 控制項，結合 TextBox 的彈性與使用者可以選擇的選項清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-107">ComboBox is an ASP.NET AJAX control that combines the flexibility of a TextBox with a list of options from which users can choose.</span></span>

<span data-ttu-id="f9124-108">本教學課程的目的是要說明 AJAX 控制項工具組 ComboBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="f9124-108">The goal of this tutorial is to explain the AJAX Control Toolkit ComboBox control.</span></span> <span data-ttu-id="f9124-109">ComboBox 的運作方式就像是標準 ASP.NET DropDownList 控制項和 TextBox 控制項之間的組合。</span><span class="sxs-lookup"><span data-stu-id="f9124-109">The ComboBox works like a combination between a standard ASP.NET DropDownList control and a TextBox control.</span></span> <span data-ttu-id="f9124-110">您可以從預先存在的專案清單中選取，或輸入新的專案。</span><span class="sxs-lookup"><span data-stu-id="f9124-110">You can either select from a pre-existing list of items or enter a new item.</span></span>

<span data-ttu-id="f9124-111">下拉式方塊類似于「自動完成控制項」擴充項，但控制項用於不同的案例。</span><span class="sxs-lookup"><span data-stu-id="f9124-111">The ComboBox is similar to the AutoComplete control extender, but the controls are used in different scenarios.</span></span> <span data-ttu-id="f9124-112">自動完成擴充項會查詢 web 服務來取得相符的專案。</span><span class="sxs-lookup"><span data-stu-id="f9124-112">The AutoComplete extender queries a web service to get matching entries.</span></span> <span data-ttu-id="f9124-113">相反地，ComboBox 控制項會以一組專案初始化。</span><span class="sxs-lookup"><span data-stu-id="f9124-113">The ComboBox control, in contrast, is initialized with a set of items.</span></span> <span data-ttu-id="f9124-114">當您使用大型 (資料集來處理大量資料時，使用 [自動完成擴充項] 是很合理的) 當您在處理一小部分的資料 (數十個汽車零件) 時，使用 ComboBox 控制項就很有意義。</span><span class="sxs-lookup"><span data-stu-id="f9124-114">Using the AutoComplete extender makes sense when you are working with a large set of data (millions of car parts) while using the ComboBox control makes sense when working with a small set of data (dozens of car parts).</span></span>

## <a name="selecting-from-a-static-list-of-items"></a><span data-ttu-id="f9124-115">從靜態專案清單中選取</span><span class="sxs-lookup"><span data-stu-id="f9124-115">Selecting from a Static List of Items</span></span>

<span data-ttu-id="f9124-116">讓我們從使用 ComboBox 控制項的簡單範例開始。</span><span class="sxs-lookup"><span data-stu-id="f9124-116">Let's start with a simple sample of using the ComboBox control.</span></span> <span data-ttu-id="f9124-117">假設您想要在下拉式清單中顯示靜態的專案清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-117">Imagine that you want to display a static list of items in a dropdown list.</span></span> <span data-ttu-id="f9124-118">不過，您想要保持開啟清單未完成的可能性。</span><span class="sxs-lookup"><span data-stu-id="f9124-118">However, you want to leave open the possibility that the list is not complete.</span></span> <span data-ttu-id="f9124-119">您想要允許使用者在清單中輸入自訂值。</span><span class="sxs-lookup"><span data-stu-id="f9124-119">You want to allow a user to enter a custom value into the list.</span></span>

<span data-ttu-id="f9124-120">我們會建立新的 ASP.NET Web Forms 頁面，並在頁面中使用 ComboBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="f9124-120">We'll create a new ASP.NET Web Forms page and use the ComboBox control in the page.</span></span> <span data-ttu-id="f9124-121">將新的 ASP.NET 網頁新增至您的專案，並切換至設計檢視。</span><span class="sxs-lookup"><span data-stu-id="f9124-121">Add the new ASP.NET page to your project and switch to Design view.</span></span>

<span data-ttu-id="f9124-122">如果您想要在頁面中使用 ComboBox 控制項，則必須將 ScriptManager 控制項加入頁面中。</span><span class="sxs-lookup"><span data-stu-id="f9124-122">If you want to use the ComboBox control in the page then you must add a ScriptManager control to the page.</span></span> <span data-ttu-id="f9124-123">將 ScriptManager 控制項從 [AJAX 擴充功能] 索引標籤底下拖曳至設計工具介面上。</span><span class="sxs-lookup"><span data-stu-id="f9124-123">Drag the ScriptManager control from beneath the AJAX Extensions tab onto the Designer surface.</span></span> <span data-ttu-id="f9124-124">您應在頁面頂端新增 ScriptManager 控制項;您可以緊接在開頭的伺服器端 &lt; 表單標記下方加入它 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="f9124-124">You should add the ScriptManager control at the top of the page; you can add it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="f9124-125">接下來，將 ComboBox 控制項拖曳至頁面上。</span><span class="sxs-lookup"><span data-stu-id="f9124-125">Next, drag the ComboBox control onto the page.</span></span> <span data-ttu-id="f9124-126">您可以使用其他 AJAX 控制項工具組控制項和控制項擴充項，在 [工具箱] 中找到 ComboBox 控制項 (查看圖 1) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-126">You can find the ComboBox control in the Toolbox with the other AJAX Control Toolkit controls and control extenders (see figure1).</span></span>

<span data-ttu-id="f9124-127">[![建立名片的簡單表單](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-127">[![Simple form for creating a business card](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="f9124-128">**圖 01**：從 [工具箱] 選取 ComboBox 控制項 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-128">**Figure 01**: Selecting the ComboBox control from the toolbox ([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image2.png))</span></span>

<span data-ttu-id="f9124-129">我們將使用 ComboBox 控制項來顯示靜態的選項清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-129">We'll use the ComboBox control to display a static list of choices.</span></span> <span data-ttu-id="f9124-130">使用者可以從下列三個選項的清單中選取特定的 spiciness 層級： [輕度]、[中] 和 [經常性 (]，請參閱 [圖 2]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-130">The user can select a particular level of spiciness for their food from a list of three choices: Mild, Medium, and Hot (see Figure 2).</span></span>

<span data-ttu-id="f9124-131">[![從靜態專案清單中選取](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-131">[![Selecting from a static list of items](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)</span></span>

<span data-ttu-id="f9124-132">**圖 02**：從靜態專案清單中選取 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-132">**Figure 02**: Selecting from a static list of items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image4.png))</span></span>

<span data-ttu-id="f9124-133">有兩種方式可以將這些選項新增至 ComboBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="f9124-133">There are two ways that you can add these choices to the ComboBox control.</span></span> <span data-ttu-id="f9124-134">首先，當您將滑鼠停留在設計檢視中的控制項上方並開啟專案編輯器時，請選取 [編輯選項] 工作選項 (請參閱 [圖 3]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-134">First, you select the Edit Options task option when hovering your mouse over the control in Design view and open the Item Editor (see Figure 3).</span></span>

<span data-ttu-id="f9124-135">[![編輯 ComboBox 專案](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-135">[![Editing ComboBox items](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)</span></span>

<span data-ttu-id="f9124-136">**圖 03**：編輯 ComboBox 專案 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-136">**Figure 03**: Editing ComboBox items([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image6.png))</span></span>

<span data-ttu-id="f9124-137">第二個選項是在來源視圖的開頭和結尾 &lt; asp： ComboBox 標記之間加入專案清單 &gt; 。</span><span class="sxs-lookup"><span data-stu-id="f9124-137">The second option is to add the list of items in between the opening and closing &lt;asp:ComboBox&gt; tags in Source view.</span></span> <span data-ttu-id="f9124-138">[清單 1] 中的頁面包含已更新專案清單的 [已更新] ComboBox。</span><span class="sxs-lookup"><span data-stu-id="f9124-138">The page in Listing 1 contains the updated ComboBox that has the list of items.</span></span>

<span data-ttu-id="f9124-139">**清單 1-靜態 .aspx**</span><span class="sxs-lookup"><span data-stu-id="f9124-139">**Listing 1 - Static.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

<span data-ttu-id="f9124-140">當您開啟 [清單 1] 中的頁面時，可以從下拉式方塊中選取其中一個預先存在的選項。</span><span class="sxs-lookup"><span data-stu-id="f9124-140">When you open the page in Listing 1, you can select one of the pre-existing options from the ComboBox.</span></span> <span data-ttu-id="f9124-141">換句話說，ComboBox 的運作方式就像是 DropDownList 控制項一樣。</span><span class="sxs-lookup"><span data-stu-id="f9124-141">In other words, the ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="f9124-142">不過，您也可以選擇輸入新的選擇 (例如，不在現有清單中的 Super Spicy) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-142">However, you also have the option of entering a new choice (for example, Super Spicy) that is not in the existing list.</span></span> <span data-ttu-id="f9124-143">因此，ComboBox 也可以像 TextBox 控制項一樣運作。</span><span class="sxs-lookup"><span data-stu-id="f9124-143">So, the ComboBox also works like a TextBox control.</span></span>

<span data-ttu-id="f9124-144">無論您是否選擇預先存在的專案，或輸入自訂專案，當您提交表單時，您的選擇都會出現在標籤控制項中。</span><span class="sxs-lookup"><span data-stu-id="f9124-144">Regardless of whether you pick a pre-existing item or you enter a custom item, when you submit the form, your choice appears in the label control.</span></span> <span data-ttu-id="f9124-145">當您提交表單時，btnSubmit \_ Click 處理常式會執行並更新標籤 (請參閱 [圖 4]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-145">When you submit the form, the btnSubmit\_Click handler executes and updates the label (see Figure 4).</span></span>

<span data-ttu-id="f9124-146">[![顯示選取的專案](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-146">[![Displaying the selected item](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)</span></span>

<span data-ttu-id="f9124-147">**圖 04**：顯示選取的專案 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-147">**Figure 04**: Displaying the selected item([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image8.png))</span></span>

<span data-ttu-id="f9124-148">ComboBox 支援與 DropDownList 控制項相同的屬性，以便在提交表單之後，用來抓取選取的專案：</span><span class="sxs-lookup"><span data-stu-id="f9124-148">The ComboBox supports the same properties as the DropDownList control for retrieving the selected item after a form is submitted:</span></span>

- <span data-ttu-id="f9124-149">SelectedItem：顯示所選取專案的 Text 屬性值。</span><span class="sxs-lookup"><span data-stu-id="f9124-149">SelectedItem.Text - Displays the value of the Text property of the selected item.</span></span>
- <span data-ttu-id="f9124-150">SelectedItem：顯示所選取專案的 Value 屬性值，或顯示在下拉式方塊中輸入的文字。</span><span class="sxs-lookup"><span data-stu-id="f9124-150">SelectedItem.Value - Displays the value of the Value property of the selected item or displays the text typed into the ComboBox.</span></span>
- <span data-ttu-id="f9124-151">SelectedValue 與 SelectedItem 相同，不同之處在于此屬性可讓您指定預設 (初始) 選取的專案。</span><span class="sxs-lookup"><span data-stu-id="f9124-151">SelectedValue - Same as SelectedItem.Value except that this property enables you to specify the default (initial) selected item.</span></span>

<span data-ttu-id="f9124-152">如果您在下拉式方塊中輸入自訂選擇，則會將自訂選項同時指派給 SelectedItem 和 SelectedItem 屬性。</span><span class="sxs-lookup"><span data-stu-id="f9124-152">If you type a custom choice into the ComboBox then the custom choice is assigned to both the SelectedItem.Text and SelectedItem.Value properties.</span></span>

## <a name="selecting-the-list-of-items-from-the-database"></a><span data-ttu-id="f9124-153">從資料庫中選取專案清單</span><span class="sxs-lookup"><span data-stu-id="f9124-153">Selecting the List of Items from the Database</span></span>

<span data-ttu-id="f9124-154">您可以從資料庫中取出下拉式方塊所顯示的專案清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-154">You can retrieve the list of items that the ComboBox displays from a database.</span></span> <span data-ttu-id="f9124-155">例如，您可以將 ComboBox 系結至 SqlDataSource 控制項、ObjectDataSource 控制項、LinqDataSource 或 EntityDataSource。</span><span class="sxs-lookup"><span data-stu-id="f9124-155">For example, you can bind the ComboBox to a SqlDataSource control, an ObjectDataSource control, a LinqDataSource, or an EntityDataSource.</span></span>

<span data-ttu-id="f9124-156">假設您想要在下拉式方塊中顯示電影清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-156">Imagine that you want to display a list of movies in a ComboBox.</span></span> <span data-ttu-id="f9124-157">您想要從電影資料庫資料表中取出電影清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-157">You want to retrieve the list of movies from the Movies database table.</span></span> <span data-ttu-id="f9124-158">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9124-158">Follow these steps:</span></span>

1. <span data-ttu-id="f9124-159">建立名為 default.aspx 的頁面</span><span class="sxs-lookup"><span data-stu-id="f9124-159">Create a page named Movies.aspx</span></span>
2. <span data-ttu-id="f9124-160">將 ScriptManager 控制項從 [工具箱] 中的 [AJAX 擴充功能] 索引標籤拖曳到頁面上，以將 ScriptManager 控制項加入頁面中。</span><span class="sxs-lookup"><span data-stu-id="f9124-160">Add a ScriptManager control to the page by dragging the ScriptManager from under the AJAX Extensions tab in the Toolbox onto the page.</span></span>
3. <span data-ttu-id="f9124-161">將 combobox 拖曳至頁面上，以將 ComboBox 控制項加入頁面中。</span><span class="sxs-lookup"><span data-stu-id="f9124-161">Add a ComboBox control to the page by dragging the ComboBox onto the page.</span></span>
4. <span data-ttu-id="f9124-162">在設計檢視中，將滑鼠停留在 ComboBox 控制項上方，然後選取 [ **選擇資料來源** ] 工作選項 (請參閱 [圖 5]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-162">In Design view, hover your mouse over the ComboBox control and select the **Choose Data Source** task option (see Figure 5).</span></span> <span data-ttu-id="f9124-163">[資料來源設定] 設定為 [已啟動]。</span><span class="sxs-lookup"><span data-stu-id="f9124-163">The Data Source Configuration Wizard is launched.</span></span>
5. <span data-ttu-id="f9124-164">在 [ **選擇資料來源** ] 步驟中，選取 [ &lt; 新增資料來源] &gt; 選項。</span><span class="sxs-lookup"><span data-stu-id="f9124-164">In the **Choose a Data Source** step, select the &lt;New data source&gt; option.</span></span>
6. <span data-ttu-id="f9124-165">在 [ **選擇資料來源類型** ] 步驟中，選取 [資料庫]。</span><span class="sxs-lookup"><span data-stu-id="f9124-165">In the **Choose a Data Source Type** step, select Database.</span></span>
7. <span data-ttu-id="f9124-166">在 [ **選擇您的資料連線** ] 步驟中，選取您的資料庫 (例如，MoviesDB .mdf) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-166">In the **Choose Your Data Connection** step, select your database (for example, MoviesDB.mdf).</span></span>
8. <span data-ttu-id="f9124-167">在 [ **將連接字串儲存到應用程式佈建檔** ] 步驟中，選取儲存連接字串的選項。</span><span class="sxs-lookup"><span data-stu-id="f9124-167">In the **Save the Connection String to the Application Configuration File** step, select the option to save your connection string.</span></span>
9. <span data-ttu-id="f9124-168">在 [ **設定 Select 語句** ] 步驟中，選取 [電影資料庫] 資料表，然後選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="f9124-168">In the **Configure the Select Statement** step, select the Movies database table and select all of the columns.</span></span>
10. <span data-ttu-id="f9124-169">在 [ **測試查詢** ] 步驟中，按一下 [完成] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9124-169">In the **Test Query** step, click the Finish button.</span></span>
11. <span data-ttu-id="f9124-170">回到 [ **選擇資料來源** ] 步驟中，選取要顯示之欄位的 [標題] 資料行，並選取 [資料] 欄位的 [識別碼] 資料行 (查看 [圖) ]。</span><span class="sxs-lookup"><span data-stu-id="f9124-170">Back in the **Choose Data Source** step, select the Title column for the field to display and the Id column for the data field (see Figure).</span></span>
12. <span data-ttu-id="f9124-171">按一下 [確定] 按鈕以關閉嚮導。</span><span class="sxs-lookup"><span data-stu-id="f9124-171">Click the OK button to close the wizard.</span></span>

<span data-ttu-id="f9124-172">[![選擇資料來源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-172">[![Choosing a data source](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)</span></span>

<span data-ttu-id="f9124-173">**圖 05**：選擇資料來源 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image10.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-173">**Figure 05**: Choosing a data source([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image10.png))</span></span>

<span data-ttu-id="f9124-174">[![選擇資料文字和值欄位](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-174">[![Choosing the data text and value fields](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)</span></span>

<span data-ttu-id="f9124-175">**圖 06**：選擇資料文字和值欄位 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image12.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-175">**Figure 06**: Choosing the data text and value fields([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image12.png))</span></span>

<span data-ttu-id="f9124-176">完成上述步驟後，ComboBox 會系結至代表電影資料庫資料表中電影的 SqlDataSource 控制項。</span><span class="sxs-lookup"><span data-stu-id="f9124-176">After you complete the steps above, the ComboBox is bound to a SqlDataSource control that represents the movies from the Movies database table.</span></span> <span data-ttu-id="f9124-177">頁面的來源看起來像 [清單 2] (我將格式化稍微) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-177">The source for the page looks like Listing 2 (I cleaned up the formatting a little bit).</span></span>

<span data-ttu-id="f9124-178">**清單 2-default.aspx**</span><span class="sxs-lookup"><span data-stu-id="f9124-178">**Listing 2 - Movies.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

<span data-ttu-id="f9124-179">請注意，ComboBox 控制項有指向 SqlDataSource 控制項的 DataSourceID 屬性。</span><span class="sxs-lookup"><span data-stu-id="f9124-179">Notice that the ComboBox control has a DataSourceID property that points to the SqlDataSource control.</span></span> <span data-ttu-id="f9124-180">當您在瀏覽器中開啟頁面時，會顯示資料庫中的電影清單 (請參閱 [圖 7]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-180">When you open the page in a browser, the list of movies from the database is displayed (see Figure 7).</span></span> <span data-ttu-id="f9124-181">您可以從清單中挑選電影，或在下拉式方塊中輸入電影來輸入新的電影。</span><span class="sxs-lookup"><span data-stu-id="f9124-181">You can either a pick a movie from the list or enter a new movie by typing the movie into the ComboBox.</span></span>

<span data-ttu-id="f9124-182">[![顯示電影清單](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-182">[![Displaying a list of movies](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)</span></span>

<span data-ttu-id="f9124-183">**圖 07**：顯示電影清單 ([按一下以觀看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image14.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-183">**Figure 07**: Displaying a list of movies([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image14.png))</span></span>

## <a name="setting-the-dropdownstyle"></a><span data-ttu-id="f9124-184">設定 DropDownStyle</span><span class="sxs-lookup"><span data-stu-id="f9124-184">Setting the DropDownStyle</span></span>

<span data-ttu-id="f9124-185">您可以使用 ComboBox DropDownStyle 屬性來變更 ComboBox 的行為。</span><span class="sxs-lookup"><span data-stu-id="f9124-185">You can use the ComboBox DropDownStyle property to change the behavior of the ComboBox.</span></span> <span data-ttu-id="f9124-186">這個屬性會接受可能的值：</span><span class="sxs-lookup"><span data-stu-id="f9124-186">This property accepts there possible values:</span></span>

- <span data-ttu-id="f9124-187">下拉式 (預設值) 當您按一下箭號時，下拉式清單會顯示下拉式清單，而您可以輸入自訂值。</span><span class="sxs-lookup"><span data-stu-id="f9124-187">DropDown - (default value) The ComboBox displays a dropdown list when you click the arrow and you can enter a custom value.</span></span>
- <span data-ttu-id="f9124-188">簡單-下拉式方塊會自動顯示下拉式清單，而您可以輸入自訂值。</span><span class="sxs-lookup"><span data-stu-id="f9124-188">Simple - The ComboBox displays a dropdown list automatically and you can enter a custom value.</span></span>
- <span data-ttu-id="f9124-189">DropDownList-下拉式方塊的運作方式就像 DropDownList 控制項一樣。</span><span class="sxs-lookup"><span data-stu-id="f9124-189">DropDownList - The ComboBox works just like a DropDownList control.</span></span>

<span data-ttu-id="f9124-190">下拉式清單和簡單的不同之處是顯示專案清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-190">The different between DropDown and Simple is when the list of items is displayed.</span></span> <span data-ttu-id="f9124-191">在簡單的情況下，當您將焦點移至下拉式方塊時，清單會立即顯示。</span><span class="sxs-lookup"><span data-stu-id="f9124-191">In the case of Simple, the list is displayed immediately when you move focus to the ComboBox.</span></span> <span data-ttu-id="f9124-192">在下拉式清單中，您必須按一下箭號以查看專案清單。</span><span class="sxs-lookup"><span data-stu-id="f9124-192">In the case of DropDown, you must click the arrow to see the list of items.</span></span>

<span data-ttu-id="f9124-193">DropDownList 值會使 ComboBox 控制項如同標準 DropDownList 控制項一樣運作。</span><span class="sxs-lookup"><span data-stu-id="f9124-193">The DropDownList value causes the ComboBox control to work just like a standard DropDownList control.</span></span> <span data-ttu-id="f9124-194">不過，這裡有一個重要的差異。</span><span class="sxs-lookup"><span data-stu-id="f9124-194">However, there is an important difference here.</span></span> <span data-ttu-id="f9124-195">舊版 Internet Explorer 會顯示具有無限 z 索引的 DropDownList 控制項，讓控制項出現在其前方的任何控制項前面。</span><span class="sxs-lookup"><span data-stu-id="f9124-195">Older versions of Internet Explorer display a DropDownList control with an infinite z-index so the control will appear in front of any control placed in front of it.</span></span> <span data-ttu-id="f9124-196">因為 ComboBox 會轉譯 HTML &lt; div &gt; 標記而非 html 選取標記，所以下拉式方塊會 &lt; &gt; 正確地遵循 z 順序。</span><span class="sxs-lookup"><span data-stu-id="f9124-196">Because the ComboBox renders an HTML &lt;div&gt; tag instead of an HTML &lt;select&gt; tag, the ComboBox correctly respects z-ordering.</span></span>

## <a name="setting-the-autocompletemode"></a><span data-ttu-id="f9124-197">設定 Autocompletemode.none</span><span class="sxs-lookup"><span data-stu-id="f9124-197">Setting the AutoCompleteMode</span></span>

<span data-ttu-id="f9124-198">您可以使用 ComboBox Autocompletemode.none 屬性來指定當有人將文字輸入 ComboBox 時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="f9124-198">You use the ComboBox AutoCompleteMode property to specify what happens when someone types text into the ComboBox.</span></span> <span data-ttu-id="f9124-199">這個屬性會接受下列可能的值：</span><span class="sxs-lookup"><span data-stu-id="f9124-199">This property accepts the following possible values:</span></span>

- <span data-ttu-id="f9124-200">None- (預設值) ComboBox 不提供任何自動完成行為。</span><span class="sxs-lookup"><span data-stu-id="f9124-200">None - (default value) The ComboBox does not provide any auto-complete behavior.</span></span>
- <span data-ttu-id="f9124-201">建議-下拉式方塊會顯示清單，並反白顯示清單中的相符專案 (請參閱 [圖 8]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-201">Suggest - The ComboBox displays the list and it highlights the matching item in the list (see Figure 8).</span></span>
- <span data-ttu-id="f9124-202">附加-下拉式方塊不會顯示清單，而會將相符的專案從清單附加到您輸入的內容 (請參閱 [圖 9]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-202">Append - The ComboBox does not display the list and it appends the matching item from the list onto what you have typed (see Figure 9).</span></span>
- <span data-ttu-id="f9124-203">SuggestAppend-下拉式方塊會顯示清單，並將清單中的相符專案附加到您輸入的內容 (請參閱 [圖 10]) 。</span><span class="sxs-lookup"><span data-stu-id="f9124-203">SuggestAppend - The ComboBox both displays the list and appends the matching item from the list onto what you have typed (see Figure 10).</span></span>

<span data-ttu-id="f9124-204">[![ComboBox 會提出建議](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-204">[![The ComboBox makes a suggestion](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)</span></span>

<span data-ttu-id="f9124-205">**圖 08**：下拉式方塊提出建議 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image16.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-205">**Figure 08**: The ComboBox makes a suggestion([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image16.png))</span></span>

<span data-ttu-id="f9124-206">[![ComboBox 附加符合的文字](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-206">[![ComboBox appends matching text](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)</span></span>

<span data-ttu-id="f9124-207">**圖 09**： ComboBox 附加相符的文字 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image18.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-207">**Figure 09**: ComboBox appends matching text([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image18.png))</span></span>

<span data-ttu-id="f9124-208">[![ComboBox 建議和附加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="f9124-208">[![The ComboBox suggests and appends](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)</span></span>

<span data-ttu-id="f9124-209">**圖 10**： ComboBox 建議和附加 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image20.png)) </span><span class="sxs-lookup"><span data-stu-id="f9124-209">**Figure 10**: The ComboBox suggests and appends([Click to view full-size image](how-do-i-use-the-combobox-control-cs/_static/image20.png))</span></span>

## <a name="summary"></a><span data-ttu-id="f9124-210">摘要</span><span class="sxs-lookup"><span data-stu-id="f9124-210">Summary</span></span>

<span data-ttu-id="f9124-211">在本教學課程中，您已瞭解如何使用 ComboBox 控制項來顯示一組固定的專案。</span><span class="sxs-lookup"><span data-stu-id="f9124-211">In this tutorial, you learned how to use the ComboBox control to display a fixed set of items.</span></span> <span data-ttu-id="f9124-212">我們將 ComboBox 控制項系結至一組靜態專案和資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="f9124-212">We bound the ComboBox control both to a static set of items and to a database table.</span></span> <span data-ttu-id="f9124-213">最後，您已瞭解如何藉由設定 DropDownStyle 和 Autocompletemode.none 屬性來修改 ComboBox 的行為。</span><span class="sxs-lookup"><span data-stu-id="f9124-213">Finally, you learned how to modify the behavior of the ComboBox by setting its DropDownStyle and AutoCompleteMode properties.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f9124-214">下一個</span><span class="sxs-lookup"><span data-stu-id="f9124-214">Next</span></span>](how-do-i-use-the-combobox-control-vb.md)
