---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用彩選器控制器 (VB) |微軟文件
author: rick-anderson
description: ColorPicker 是 ASP.NET AJAX 擴充器,在彈出視窗控制項中提供客戶端選色功能和 UI。 它可以附加到任何ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: c373102665ac17020ca8d5f14d3488a874bb68de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542842"
---
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="1caa4-104">使用彩選擇器控制器 (VB)</span><span class="sxs-lookup"><span data-stu-id="1caa4-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="1caa4-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1caa4-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1caa4-106">ColorPicker 是 ASP.NET AJAX 擴充器,在彈出視窗控制項中提供客戶端選色功能和 UI。</span><span class="sxs-lookup"><span data-stu-id="1caa4-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="1caa4-107">它可以附加到任何ASP.NET文本框控件。</span><span class="sxs-lookup"><span data-stu-id="1caa4-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="1caa4-108">它。</span><span class="sxs-lookup"><span data-stu-id="1caa4-108">It.</span></span>

<span data-ttu-id="1caa4-109">本教學的目的是解釋如何使用 AJAX 控制項工具套件 ColorPicker 控制件延伸器。</span><span class="sxs-lookup"><span data-stu-id="1caa4-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="1caa4-110">ColorPicker 控制元件延伸器顯示一個彈出對話框,讓您能夠選擇顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="1caa4-111">當您要為使用者提供直觀的使用者介面以選擇顏色時,ColorPicker 非常有用。</span><span class="sxs-lookup"><span data-stu-id="1caa4-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="1caa4-112">使用彩選擇器控制器延伸器延伸文字框控制項</span><span class="sxs-lookup"><span data-stu-id="1caa4-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="1caa4-113">例如,假設您想要創建一個網站,使訪問者能夠創建自定義的名片。</span><span class="sxs-lookup"><span data-stu-id="1caa4-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="1caa4-114">存取者可以輸入名片的文字並選擇顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="1caa4-115">清單1中的ASP.NET頁包含兩個名為 txtCardText 和 txtCardColor 的 TextBox 控制項。</span><span class="sxs-lookup"><span data-stu-id="1caa4-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="1caa4-116">提交表單時,將顯示所選值(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="1caa4-117">[![建立名片的簡單表單](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1caa4-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="1caa4-118">**圖01:** 建立名片的簡單表單([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1caa4-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="1caa4-119">**清單 1 - 建立卡.aspx**</span><span class="sxs-lookup"><span data-stu-id="1caa4-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="1caa4-120">清單1中的表單有效,但它不能提供出色的用戶體驗。</span><span class="sxs-lookup"><span data-stu-id="1caa4-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="1caa4-121">使用者必須鍵入文字框中的顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="1caa4-122">如果使用者想要專用顏色(例如,只是豌豆綠色的正確陰影),則用戶必須在沒有任何幫助的情況下找出 HTML 顏色代碼。</span><span class="sxs-lookup"><span data-stu-id="1caa4-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="1caa4-123">您可以使用 ColorPicker 控制元件擴充器來創建更好的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="1caa4-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="1caa4-124">將焦點移至 TextBox 控制件時,顏色選取器將顯示顏色對話框(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="1caa4-125">[![彩工控制延伸器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1caa4-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="1caa4-126">**圖 02**: 彩選擇器控制元件延伸器 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="1caa4-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="1caa4-127">您需要完成兩個步驟才能將 ColorPicker 控制元件延伸器與清單 1 中的表單一起使用:</span><span class="sxs-lookup"><span data-stu-id="1caa4-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="1caa4-128">將文稿管理員加入頁面</span><span class="sxs-lookup"><span data-stu-id="1caa4-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="1caa4-129">將彩選擇器控制器</span><span class="sxs-lookup"><span data-stu-id="1caa4-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="1caa4-130">使用 ColorPicker 之前,必須向頁面加入文稿管理員。</span><span class="sxs-lookup"><span data-stu-id="1caa4-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="1caa4-131">添加文本管理器的好地方就在打開的伺服器端&lt;表&gt;單 標記的正下方。</span><span class="sxs-lookup"><span data-stu-id="1caa4-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="1caa4-132">您可以將文稿管理器從工具箱拖到頁面上(文稿管理器位於 AJAX 擴展選項卡下)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="1caa4-133">或者,您可以在開啟伺服器端表單標籤下的源檢視中鍵入以下標記:</span><span class="sxs-lookup"><span data-stu-id="1caa4-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="1caa4-134">&lt;asp:文稿管理員 ID="文稿管理員1"運行 at="伺服器" /&gt;</span><span class="sxs-lookup"><span data-stu-id="1caa4-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="1caa4-135">將 ColorPicker 控制元件擴展器添加到頁面的最簡單方法是在「設計檢視」 中。</span><span class="sxs-lookup"><span data-stu-id="1caa4-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="1caa4-136">如果將滑鼠懸停在 txtCardColor TextBox 上,將顯示一個智慧任務選項,使您能夠添加擴展器(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="1caa4-137">如果選擇此選項,將顯示擴展器嚮導(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="1caa4-138">[![新增延伸器](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1caa4-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="1caa4-139">**圖 03**: 新增延伸器 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1caa4-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="1caa4-140">[![使用延伸器精靈選擇控制器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1caa4-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="1caa4-141">**圖 04**:使用延伸器精靈選擇控制元件延伸器([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="1caa4-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="1caa4-142">您可以選擇顏色選取器延伸器,以便使用顏色選取器延伸器延伸 txtCardColor 文字盒。</span><span class="sxs-lookup"><span data-stu-id="1caa4-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="1caa4-143">按一下 [確定] 關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1caa4-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="1caa4-144">進行這些更改後,頁面的源類似於清單 2。</span><span class="sxs-lookup"><span data-stu-id="1caa4-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="1caa4-145">**清單2 - CreateCard.aspx(含彩選器)**</span><span class="sxs-lookup"><span data-stu-id="1caa4-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="1caa4-146">請注意,該頁面現在包含一個顏色選取器擴展器控制件,該控件直接顯示在 txtCardColor 文字盒控制項的正下方。</span><span class="sxs-lookup"><span data-stu-id="1caa4-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="1caa4-147">顏色選取器延伸器控制項延伸 txtCardColor 控制項,以便顯示顏色選取器對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1caa4-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="1caa4-148">使用按鈕啟動顏色選擇器對話框</span><span class="sxs-lookup"><span data-stu-id="1caa4-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="1caa4-149">色彩選擇器延伸器支援以下屬性:</span><span class="sxs-lookup"><span data-stu-id="1caa4-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="1caa4-150">彈出ButtonId - 頁面上導致顏色選取器對話框顯示的按鈕的 ID。</span><span class="sxs-lookup"><span data-stu-id="1caa4-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="1caa4-151">彈出位置 - 顏色選取器對話框相對於目標控制項的位置。</span><span class="sxs-lookup"><span data-stu-id="1caa4-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="1caa4-152">可能的值是「絕對」、「中心」、「左下」、「右下角」、「左上」、「右」、「左」(預設值為」左下」。</span><span class="sxs-lookup"><span data-stu-id="1caa4-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="1caa4-153">範例控制代碼 - 顯示選取的顏色的控制項的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1caa4-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="1caa4-154">選擇顏色 - 顏色選擇器選擇的初始顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="1caa4-155">您可以使用這些屬性自定義顏色選取器對話框的顯示方式以及選取顏色的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="1caa4-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="1caa4-156">清單3中的頁面說明瞭如何使用其中幾個屬性。</span><span class="sxs-lookup"><span data-stu-id="1caa4-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="1caa4-157">**清單3 - 建立卡按鈕.aspx**</span><span class="sxs-lookup"><span data-stu-id="1caa4-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="1caa4-158">清單3中的頁面包括「選取顏色」按鈕(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="1caa4-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="1caa4-159">按下此按鈕時,顏色選取器對話框將顯示在 TextBox 上方。</span><span class="sxs-lookup"><span data-stu-id="1caa4-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="1caa4-160">如果從對話框中選擇顏色,則選取顏色將顯示為 lblSample 標籤控制項的背景顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="1caa4-161">"顏色選擇器彈出按鈕ID"屬性用於將"拾取顏色"按鈕與"顏色選取器"擴充器相關聯。</span><span class="sxs-lookup"><span data-stu-id="1caa4-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="1caa4-162">當您提供 PopupButtonID 屬性的值時,當目標控制項具有焦點時,顏色選取器對話方塊將不再顯示。</span><span class="sxs-lookup"><span data-stu-id="1caa4-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="1caa4-163">您必須按下這個按鈕才能顯示對話框。</span><span class="sxs-lookup"><span data-stu-id="1caa4-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="1caa4-164">SampleControlID 屬性用於將顯示所選顏色的控制項與顏色選取器相關聯。</span><span class="sxs-lookup"><span data-stu-id="1caa4-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="1caa4-165">顏色選擇器將此控制的背景顏色改變為目前選擇的顏色。</span><span class="sxs-lookup"><span data-stu-id="1caa4-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="1caa4-166">[![使用按鈕顯示顏色選擇器對話框](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1caa4-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="1caa4-167">**圖 05**: 使用按鈕顯示顏色選擇器對話框 ([按下以檢視全尺寸影像](using-the-colorpicker-control-extender-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="1caa4-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="1caa4-168">總結</span><span class="sxs-lookup"><span data-stu-id="1caa4-168">Summary</span></span>

<span data-ttu-id="1caa4-169">在本教學中,您學習了如何使用 ColorPicker 控制元件擴展器來顯示彈出顏色選取器對話框。</span><span class="sxs-lookup"><span data-stu-id="1caa4-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="1caa4-170">首先,我們檢查了在焦點移動到 TextBox 控件時如何顯示對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1caa4-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="1caa4-171">接下來,您學習了如何在按一下該按鈕時創建顯示顏色選取器對話框的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1caa4-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1caa4-172">上一步</span><span class="sxs-lookup"><span data-stu-id="1caa4-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
