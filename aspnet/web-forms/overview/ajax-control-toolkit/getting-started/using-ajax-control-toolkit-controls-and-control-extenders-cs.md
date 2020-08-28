---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: '使用 AJAX 控制項工具組控制項和控制項擴充項 (c # ) |Microsoft Docs'
author: rick-anderson
description: 瞭解如何將 AJAX 控制項工具組控制項和擴充項加入至 ASP.NET 網頁。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 48c8479fce6d121b8a4f03d972ac4117ed974958
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044502"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="fda87-103">使用 AJAX Control Toolkit 控制項及控制項擴充項 (C#)</span><span class="sxs-lookup"><span data-stu-id="fda87-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="fda87-104">由 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fda87-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fda87-105">瞭解如何將 AJAX 控制項工具組控制項和擴充項加入至 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="fda87-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="fda87-106">AJAX 控制項工具組包含一組控制項和控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="fda87-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="fda87-107">在這個簡短的教學課程中，您將瞭解如何將控制項和控制項擴充項加入至 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="fda87-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="fda87-108">如需有關如何安裝 AJAX 控制項工具組，以及將 AJAX 控制項工具組新增至 Visual Studio/Visual Web Developer 工具箱的指示，請參閱教學課程開始中的 [Ajax 控制項工具](get-started-with-the-ajax-control-toolkit-cs.md)組。</span><span class="sxs-lookup"><span data-stu-id="fda87-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="fda87-109">使用 AJAX 控制項工具組控制項</span><span class="sxs-lookup"><span data-stu-id="fda87-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="fda87-110">AJAX 控制項工具組控制項的運作方式就像一般的 ASP.NET 控制項一樣。</span><span class="sxs-lookup"><span data-stu-id="fda87-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="fda87-111">您可以將控制項從 [工具箱] 拖曳至 ASP.NET 網頁。</span><span class="sxs-lookup"><span data-stu-id="fda87-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="fda87-112">您可以在設計檢視或來源視圖的頁面中加入控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="fda87-113">使用 AJAX 控制項工具組中的控制項時，有一項特殊需求。</span><span class="sxs-lookup"><span data-stu-id="fda87-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="fda87-114">頁面必須包含 ScriptManager 控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="fda87-115">ScriptManager 控制項負責包含 AJAX 控制項工具組控制項所需的所有必要 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="fda87-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="fda87-116">例如，[AJAX 控制項工具組] 索引標籤包含一個名為 Editor 控制項的控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="fda87-117">此控制項會顯示豐富的 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="fda87-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="fda87-118">遵循下列步驟將編輯器控制項新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="fda87-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="fda87-119">建立新的 ASP.NET 網頁，名為 ShowEditor .aspx</span><span class="sxs-lookup"><span data-stu-id="fda87-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="fda87-120">從 [工具箱] 的 [AJAX 擴充功能] 索引標籤底下選取 ScriptManager 控制項，然後將控制項拖曳到頁面上。</span><span class="sxs-lookup"><span data-stu-id="fda87-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="fda87-121">從 [工具箱] 的 [AJAX 控制項工具組] 索引標籤底下選取編輯器控制項，然後將控制項拖曳到頁面上 (見 [圖 1]) 。</span><span class="sxs-lookup"><span data-stu-id="fda87-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="fda87-122">設計工具看起來應該如圖2所示。</span><span class="sxs-lookup"><span data-stu-id="fda87-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="fda87-123">選取功能表選項 [ **Debug]、[開始** ] 或按 F5 鍵，以執行網站。</span><span class="sxs-lookup"><span data-stu-id="fda87-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="fda87-124">您應該會看到 [圖 3] 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="fda87-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="fda87-125">[![選取 HTML 編輯器控制項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="fda87-126">**圖 01**：選取 HTML 編輯器控制項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>

<span data-ttu-id="fda87-127">[![使用 ScriptManager 和編輯控制項 Visual Studio 設計工具](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="fda87-128">**圖 02**：使用 ScriptManager 和編輯控制項 Visual Studio 設計工具 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>

<span data-ttu-id="fda87-129">[![DisplayEditor .aspx 頁面](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="fda87-130">**圖 03**： DisplayEditor .aspx 頁面 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="fda87-131">使用 AJAX 控制項工具組控制項擴充項</span><span class="sxs-lookup"><span data-stu-id="fda87-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="fda87-132">AJAX 控制項工具組也包含控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="fda87-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="fda87-133">如其名所示，控制項擴充項會擴充現有控制項的功能。</span><span class="sxs-lookup"><span data-stu-id="fda87-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="fda87-134">例如，項 confirmbutton 控制項擴充項會擴充標準 ASP.NET 按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="fda87-135">擴充項會變更按鈕控制項的行為，如此當您按一下按鈕時，按鈕就會顯示確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fda87-135">The extender changes the Button control's behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="fda87-136">控制項擴充項和 AJAX 控制項工具組控制項一樣，都需要 ScriptManager 控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="fda87-137">在頁面中開始使用控制項擴充項之前，您必須先將 ScriptManager 控制項加入頁面中。</span><span class="sxs-lookup"><span data-stu-id="fda87-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="fda87-138">遵循下列步驟以使用項 confirmbutton 控制項擴充項：</span><span class="sxs-lookup"><span data-stu-id="fda87-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="fda87-139">建立新的 ASP.NET 網頁，名為 ShowConfirmButton .aspx</span><span class="sxs-lookup"><span data-stu-id="fda87-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="fda87-140">從 [AJAX 擴充功能] 索引標籤底下，將控制項拖曳至頁面上，以將 ScriptManager 控制項加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="fda87-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="fda87-141">將 [標準] 按鈕控制項從 [工具箱] 中的 [標準] 索引標籤下拖曳至設計工具介面，以將其加入至頁面。</span><span class="sxs-lookup"><span data-stu-id="fda87-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="fda87-142">按一下 [ **加入** 擴充項工作] 選項 (參閱 [圖 4]) 。</span><span class="sxs-lookup"><span data-stu-id="fda87-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="fda87-143">在 [選擇擴充項] 對話方塊中，選取 [ConfirmButtonExtender (參閱 [圖 5]) 然後按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fda87-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="fda87-144">選取設計工具中的 [Button] 控制項，然後展開屬性視窗中的 [Button1]、[Button1 \_ ConfirmButtonExtender] 節點 (看到 [圖 6]) 。</span><span class="sxs-lookup"><span data-stu-id="fda87-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="fda87-145">指派值 *' 真的？ '*</span><span class="sxs-lookup"><span data-stu-id="fda87-145">Assign the value *'Really?'*</span></span> <span data-ttu-id="fda87-146">ConfirmText 屬性。</span><span class="sxs-lookup"><span data-stu-id="fda87-146">to the ConfirmText property.</span></span>
7. <span data-ttu-id="fda87-147">選取功能表選項 [Debug]、[ **開始** ] 或按 F5 鍵來執行頁面。</span><span class="sxs-lookup"><span data-stu-id="fda87-147">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="fda87-148">[![新增擴充項工作選項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-148">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="fda87-149">**圖 04**： [加入擴充項工作] 選項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-149">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>

<span data-ttu-id="fda87-150">[![選取項 confirmbutton 控制項擴充項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-150">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="fda87-151">**圖 05**：選取項 confirmbutton 控制項擴充項 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-151">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>

<span data-ttu-id="fda87-152">[![設定項 confirmbutton 屬性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-152">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="fda87-153">**圖 06**：設定項 confirmbutton 屬性 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-153">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>

<span data-ttu-id="fda87-154">當頁面開啟時，您應該會看到一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="fda87-154">When the page opens, you should see a button.</span></span> <span data-ttu-id="fda87-155">當您按一下按鈕時，您會在 [圖 7] 中看到確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fda87-155">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="fda87-156">[![顯示確認對話方塊](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="fda87-156">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="fda87-157">**圖 07**：顯示確認對話方塊 ([按一下以查看完整大小的影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png)) </span><span class="sxs-lookup"><span data-stu-id="fda87-157">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>

<span data-ttu-id="fda87-158">請注意，您通常不會將控制項擴充項拖曳到頁面上。</span><span class="sxs-lookup"><span data-stu-id="fda87-158">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="fda87-159">相反地，您可以使用 [ **加入** 擴充項工作] 選項，將擴充項加入至已加入至頁面的控制項。</span><span class="sxs-lookup"><span data-stu-id="fda87-159">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="fda87-160">另外也請注意，您可以藉由開啟要擴充之控制項的屬性工作表來設定控制項擴充項屬性。</span><span class="sxs-lookup"><span data-stu-id="fda87-160">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="fda87-161">單一 ASP.NET 控制項可以由多個控制項擴充項延伸。</span><span class="sxs-lookup"><span data-stu-id="fda87-161">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="fda87-162">要擴充之控制項的屬性工作表將會列出與控制項相關聯的所有控制項擴充項。</span><span class="sxs-lookup"><span data-stu-id="fda87-162">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fda87-163">[上一個](get-started-with-the-ajax-control-toolkit-cs.md) 
> [下一步](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="fda87-163">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
