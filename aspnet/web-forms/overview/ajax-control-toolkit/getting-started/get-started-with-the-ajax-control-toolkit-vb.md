---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: 開始使用 AJAX Control Toolkit (VB) |Microsoft Docs
author: microsoft
description: 了解所有您需要知道若要開始使用 AJAX Control Toolkit。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 0b00fd5dc12c21183ef61d7ebb23211a1aa4719e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59418959"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="d08e2-103">開始使用 AJAX Control Toolkit (VB)</span><span class="sxs-lookup"><span data-stu-id="d08e2-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="d08e2-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d08e2-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d08e2-105">了解所有您需要知道若要開始使用 AJAX Control Toolkit。</span><span class="sxs-lookup"><span data-stu-id="d08e2-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="d08e2-106">AJAX Control Toolkit 包含 30 個以上可用的控制項，您可以使用 ASP.NET 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="d08e2-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="d08e2-107">在本教學課程中，您將了解如何下載 AJAX Control Toolkit 和工具組將控制項新增到您的 Visual Studio/Visual Web Developer Express 工具箱。</span><span class="sxs-lookup"><span data-stu-id="d08e2-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="d08e2-108">下載 AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="d08e2-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="d08e2-109">[AJAX Control Toolkit](http://devexpress.com/act)由 ASP.NET 社群和 ASP.NET 團隊的成員所開發的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="d08e2-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>


[![D<span data-ttu-id="d08e2-110">ownloading AJAX Control Toolkit]</span><span class="sxs-lookup"><span data-stu-id="d08e2-110">ownloading the AJAX Control Toolkit]</span></span>(get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

<span data-ttu-id="d08e2-111">**圖 01**:下載 AJAX Control Toolkit ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d08e2-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>


<span data-ttu-id="d08e2-112">您可以下載檔案之後，您需要解除封鎖檔案。</span><span class="sxs-lookup"><span data-stu-id="d08e2-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="d08e2-113">以滑鼠右鍵按一下檔案，選取 內容，按一下 **解除封鎖**按鈕 （請參閱 圖 2）。</span><span class="sxs-lookup"><span data-stu-id="d08e2-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


[![U<span data-ttu-id="d08e2-114">nblocking AJAX 控制項工具組 ZIP 檔案]</span><span class="sxs-lookup"><span data-stu-id="d08e2-114">nblocking the AJAX Control Toolkit ZIP file]</span></span>(get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

<span data-ttu-id="d08e2-115">**圖 02**:解除封鎖的 AJAX 控制項工具組 ZIP 檔案 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="d08e2-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>


<span data-ttu-id="d08e2-116">解除封鎖檔案之後，您可以將檔案解壓縮：以滑鼠右鍵按一下檔案，然後選取**擷取所有**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="d08e2-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="d08e2-117">現在，我們已準備好將此工具組新增至 Visual Studio/Visual Web Developer 工具箱。</span><span class="sxs-lookup"><span data-stu-id="d08e2-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="d08e2-118">新增至工具箱的 AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="d08e2-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="d08e2-119">使用 AJAX Control Toolkit 最簡單方式是將此工具組新增至您的 Visual Studio/Visual Web Developer 工具箱 （請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="d08e2-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="d08e2-120">這樣一來，您可以只將 toolkit 控制項拖曳至頁面時您想要使用它。</span><span class="sxs-lookup"><span data-stu-id="d08e2-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


[![A<span data-ttu-id="d08e2-121">JAX Control Toolkit 會出現在 [工具箱]</span><span class="sxs-lookup"><span data-stu-id="d08e2-121">JAX Control Toolkit appears in toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

<span data-ttu-id="d08e2-122">**圖 03**:AJAX Control Toolkit 會出現在 [工具箱] ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d08e2-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>


<span data-ttu-id="d08e2-123">首先，您要新增至工具箱的 AJAX Control Toolkit 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d08e2-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="d08e2-124">請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d08e2-124">Follow these steps.</span></span>

1. <span data-ttu-id="d08e2-125">選取功能表選項的檔案，新的網站，以建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="d08e2-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="d08e2-126">按兩下 [方案總管] 視窗中的 Default.aspx，在編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="d08e2-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="d08e2-127">以滑鼠右鍵按一下 一般 索引標籤下方的 工具箱，然後選取功能表選項**加入索引標籤**（請參閱 圖 4）。</span><span class="sxs-lookup"><span data-stu-id="d08e2-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="d08e2-128">輸入名為 AJAX Control Toolkit 中的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d08e2-128">Enter a new tab named AJAX Control Toolkit.</span></span>


[![A<span data-ttu-id="d08e2-129">dding 新索引標籤]</span><span class="sxs-lookup"><span data-stu-id="d08e2-129">dding a new tab]</span></span>(get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

<span data-ttu-id="d08e2-130">**圖 04**:將新的索引標籤 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="d08e2-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>


<span data-ttu-id="d08e2-131">接下來，您需要將 AJAX Control Toolkit 控制項新增至新的索引標籤。請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d08e2-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="d08e2-132">以滑鼠右鍵按一下下方的 [AJAX Control Toolkit] 索引標籤，然後選取功能表選項**選擇的項目 （請參閱 [圖 5]）**。</span><span class="sxs-lookup"><span data-stu-id="d08e2-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="d08e2-133">瀏覽至您解壓縮 AJAX Control Toolkit 和選取 AjaxControlToolkit.dll 組件的位置。</span><span class="sxs-lookup"><span data-stu-id="d08e2-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


[![C<span data-ttu-id="d08e2-134">要加入至工具箱的選擇項目]</span><span class="sxs-lookup"><span data-stu-id="d08e2-134">hoose items to add to the toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

<span data-ttu-id="d08e2-135">**圖 05**:選擇要加入至工具箱項目 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="d08e2-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>


<span data-ttu-id="d08e2-136">完成這些步驟之後，所有的工具組控制項都會顯示在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="d08e2-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="d08e2-137">升級至新版本的工具組</span><span class="sxs-lookup"><span data-stu-id="d08e2-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="d08e2-138">如果您已使用的版本還舊的工具組，而且現在需要將移至較新的版本是建議的步驟：</span><span class="sxs-lookup"><span data-stu-id="d08e2-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="d08e2-139">二進位檔-從您網站的 Bin 資料夾刪除 AjaxControlToolkit.dll 組件的舊版本。</span><span class="sxs-lookup"><span data-stu-id="d08e2-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="d08e2-140">工具箱項目-刪除 AJAX Control Toolkit 索引標籤，並遵循上述步驟，以重新建立具有新版 AjaxControlToolkit.dll 組件的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d08e2-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d08e2-141">[上一頁](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一頁](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d08e2-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
