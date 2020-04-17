---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: 使用 AJAX 控制工具套件控制並控制延伸器 (C#) |微軟文件
author: rick-anderson
description: 瞭解如何將 AJAX 控制工具套件控制項和擴展器添加到ASP.NET頁。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 5729db63f831b74ca37c573791c53c39265c1f39
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543713"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="57798-103">使用 AJAX Control Toolkit 控制項及控制項擴充項 (C#)</span><span class="sxs-lookup"><span data-stu-id="57798-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="57798-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="57798-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="57798-105">瞭解如何將 AJAX 控制工具套件控制項和擴展器添加到ASP.NET頁。</span><span class="sxs-lookup"><span data-stu-id="57798-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>

<span data-ttu-id="57798-106">AJAX 控制工具套件包含一元件和控制擴展器。</span><span class="sxs-lookup"><span data-stu-id="57798-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="57798-107">在本教學中,您將瞭解如何將控制器和控制擴展器添加到ASP.NET頁。</span><span class="sxs-lookup"><span data-stu-id="57798-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="57798-108">有關安裝 AJAX 控制工具組並將 AJAX 控制工具套件添加到可視化工作室/可視化 Web 開發人員工具組的說明,請參閱[有關 AJAX 控制項工具組入門](get-started-with-the-ajax-control-toolkit-cs.md)教學。</span><span class="sxs-lookup"><span data-stu-id="57798-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>

## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="57798-109">使用 AJAX 控制工具套件控制項</span><span class="sxs-lookup"><span data-stu-id="57798-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="57798-110">AJAX 控制工具套件控制項的工作方式與普通ASP.NET控件類似。</span><span class="sxs-lookup"><span data-stu-id="57798-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="57798-111">您可以將控制式從工具匣拖到ASP.NET頁上。</span><span class="sxs-lookup"><span data-stu-id="57798-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="57798-112">您可以在「設計」檢視或「源」檢視中將控制件添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="57798-113">使用 AJAX 控制工具套件中的控制件時有一個特殊要求。</span><span class="sxs-lookup"><span data-stu-id="57798-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="57798-114">該頁必須包含腳本管理器控制項。</span><span class="sxs-lookup"><span data-stu-id="57798-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="57798-115">文稿管理器控制項負責包括 AJAX 控制工具套件控制件所需的所有 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="57798-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="57798-116">例如,AJAX 控制件工具組選項卡包括名為編輯器控制項的控制項。</span><span class="sxs-lookup"><span data-stu-id="57798-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="57798-117">此控制項顯示豐富的 HTML 編輯器。</span><span class="sxs-lookup"><span data-stu-id="57798-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="57798-118">依以下步驟將編輯器控制項</span><span class="sxs-lookup"><span data-stu-id="57798-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="57798-119">建立新ASP.NET頁面名為 ShowEditor.aspx</span><span class="sxs-lookup"><span data-stu-id="57798-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="57798-120">從工具箱中的 AJAX 擴展選項卡下方選擇腳本管理器控制項,並將該控制項拖到頁面上。</span><span class="sxs-lookup"><span data-stu-id="57798-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="57798-121">從工具箱中的 AJAX 控制工具組選項卡下方選擇編輯器控制件,並將控制項拖到頁面上(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="57798-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="57798-122">設計器應如圖 2 所示。</span><span class="sxs-lookup"><span data-stu-id="57798-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="57798-123">通過選擇功能表選項 **「除錯、「開始除錯**」或點擊 F5 鍵來運行網站。</span><span class="sxs-lookup"><span data-stu-id="57798-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="57798-124">您應該會看到圖 3 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-124">You should see the page in Figure 3.</span></span>

<span data-ttu-id="57798-125">[![選擇 HTML 編輯器控制項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="57798-125">[![Selecting the HTML Editor control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)</span></span>

<span data-ttu-id="57798-126">**圖 01**:選擇 HTML 編輯器控制件([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="57798-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>

<span data-ttu-id="57798-127">[![具有文稿管理員及編輯控制項的視覺化工作室設計器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="57798-127">[![Visual Studio Designer with ScriptManager and Edit control](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)</span></span>

<span data-ttu-id="57798-128">**圖 02**: 具有文稿管理員與編輯控制項的視覺化工作室設計器([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="57798-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>

<span data-ttu-id="57798-129">[![顯示編輯器.aspx 頁面](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="57798-129">[![The DisplayEditor.aspx page](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)</span></span>

<span data-ttu-id="57798-130">**圖 03**: 顯示編輯器.aspx 頁面([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="57798-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>

## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="57798-131">使用 AJAX 控制工具套件控制擴充器</span><span class="sxs-lookup"><span data-stu-id="57798-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="57798-132">AJAX 控制工具組還包含控制擴展器。</span><span class="sxs-lookup"><span data-stu-id="57798-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="57798-133">顧名思義,控件擴展器擴展了現有控制項的功能。</span><span class="sxs-lookup"><span data-stu-id="57798-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="57798-134">例如,「確認按鈕」控制器擴展器擴展了標準ASP.NET按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="57798-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="57798-135">擴展程式更改按鈕控制件的行為,以便按一下按鈕時顯示確認對話方塊。</span><span class="sxs-lookup"><span data-stu-id="57798-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="57798-136">控制項延伸器(與 AJAX 控制項工具套件控制件一樣)需要文稿管理器控制項。</span><span class="sxs-lookup"><span data-stu-id="57798-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="57798-137">在開始使用頁面中的控制器之前,必須將文稿管理器控制項添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="57798-138">依以下步驟使用確認按鈕控制元件延伸器:</span><span class="sxs-lookup"><span data-stu-id="57798-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="57798-139">創建新ASP.NET頁面名為"顯示確認按鈕.aspx"</span><span class="sxs-lookup"><span data-stu-id="57798-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="57798-140">通過將控制項從 AJAX 擴充選項卡下方拖曳到頁面上,將文本管理器控制件添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="57798-141">通過將「按鈕」從工具箱中的「標準」選項卡下方拖動到「設計器」圖面,將標準按鈕控制項添加到頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="57798-142">按下 **「新增延伸器**」工作選項(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="57798-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="57798-143">在「選擇擴展器」對話框中,選擇「確認按鈕擴展器」(參見圖 5),然後單擊"確定"按鈕。</span><span class="sxs-lookup"><span data-stu-id="57798-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="57798-144">選擇設計器中的「按鈕」控制器並展開「屬性」視窗中的\_Button1 確認按鈕擴展器節點(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="57798-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="57798-145">將值 *「真的?"* 分配給」確認文本"</span><span class="sxs-lookup"><span data-stu-id="57798-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="57798-146">通過選擇功能表選項 **「調試」、「開始調試」** 或點擊 F5 鍵來運行頁面。</span><span class="sxs-lookup"><span data-stu-id="57798-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>

<span data-ttu-id="57798-147">[![新增擴充器工作選項](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="57798-147">[![The Add Extender task option](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)</span></span>

<span data-ttu-id="57798-148">**圖 04**: 新增延伸器工作選項([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="57798-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>

<span data-ttu-id="57798-149">[![選擇確認按鍵控制延伸器](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="57798-149">[![Selecting the ConfirmButton control extender](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)</span></span>

<span data-ttu-id="57798-150">**圖 05**: 選擇確認按鈕控制元件延伸器([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="57798-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>

<span data-ttu-id="57798-151">[![設定確認按鈕屬性](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="57798-151">[![Setting a ConfirmButton property](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)</span></span>

<span data-ttu-id="57798-152">**圖 06**: 設定確認按鈕屬性([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="57798-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>

<span data-ttu-id="57798-153">打開頁面時,應看到一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="57798-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="57798-154">按下這個按鈕時,您將獲得圖 7 中的確認對話框。</span><span class="sxs-lookup"><span data-stu-id="57798-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>

<span data-ttu-id="57798-155">[![顯示確認對話框](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="57798-155">[![Displaying the confirmation dialog](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)</span></span>

<span data-ttu-id="57798-156">**圖 07**: 顯示確認對話框([按下以檢視全尺寸影像](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="57798-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>

<span data-ttu-id="57798-157">請注意,您通常不會將控制器拖動到頁面上。</span><span class="sxs-lookup"><span data-stu-id="57798-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="57798-158">相反,您可以使用 **「新增延伸器**」工作選項將擴展器添加到已添加到頁面的控制項。</span><span class="sxs-lookup"><span data-stu-id="57798-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="57798-159">此外,請注意,通過打開要擴展的控制項的屬性表來設置控制元件擴展器屬性。</span><span class="sxs-lookup"><span data-stu-id="57798-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="57798-160">單個ASP.NET控件可以通過多個控制元件擴展器進行擴展。</span><span class="sxs-lookup"><span data-stu-id="57798-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="57798-161">要擴展的控制項的屬性表將列出與控制項關聯的所有控制元件擴展器。</span><span class="sxs-lookup"><span data-stu-id="57798-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="57798-162">[前一個](get-started-with-the-ajax-control-toolkit-cs.md)
> [下一個](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="57798-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
