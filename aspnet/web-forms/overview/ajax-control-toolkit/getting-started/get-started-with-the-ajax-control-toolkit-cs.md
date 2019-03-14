---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 開始使用 AJAX Control Toolkit (C#) |Microsoft Docs
author: microsoft
description: 了解所有您需要知道若要開始使用 AJAX Control Toolkit。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 6ecf716b78a789ca72e8b35e0be3e1fd0b957052
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57052455"
---
<a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="fbb30-103">開始使用 AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="fbb30-103">Get Started with the AJAX Control Toolkit (C#)</span></span>
====================
<span data-ttu-id="fbb30-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fbb30-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fbb30-105">了解所有您需要知道若要開始使用 AJAX Control Toolkit。</span><span class="sxs-lookup"><span data-stu-id="fbb30-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="fbb30-106">AJAX Control Toolkit 包含 30 個以上可用的控制項，您可以使用 ASP.NET 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="fbb30-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="fbb30-107">在本教學課程中，您將了解如何下載 AJAX Control Toolkit 和工具組將控制項新增到您的 Visual Studio/Visual Web Developer Express 工具箱。</span><span class="sxs-lookup"><span data-stu-id="fbb30-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="fbb30-108">下載 AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="fbb30-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="fbb30-109">[AJAX Control Toolkit](http://devexpress.com/act)由 ASP.NET 社群和 ASP.NET 團隊的成員所開發的開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="fbb30-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


<span data-ttu-id="fbb30-110">[![下載 AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fbb30-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="fbb30-111">**圖 01**:下載 AJAX Control Toolkit ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="fbb30-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="fbb30-112">您可以下載檔案之後，您需要解除封鎖檔案。</span><span class="sxs-lookup"><span data-stu-id="fbb30-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="fbb30-113">以滑鼠右鍵按一下檔案，選取 內容，按一下 **解除封鎖**按鈕 （請參閱 圖 2）。</span><span class="sxs-lookup"><span data-stu-id="fbb30-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


<span data-ttu-id="fbb30-114">[![解除封鎖的 AJAX 控制項工具組 ZIP 檔案](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fbb30-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="fbb30-115">**圖 02**:解除封鎖的 AJAX 控制項工具組 ZIP 檔案 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="fbb30-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="fbb30-116">解除封鎖檔案之後，您可以將檔案解壓縮：以滑鼠右鍵按一下檔案，然後選取**擷取所有**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="fbb30-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="fbb30-117">現在，我們已準備好將此工具組新增至 Visual Studio/Visual Web Developer 工具箱。</span><span class="sxs-lookup"><span data-stu-id="fbb30-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="fbb30-118">新增至工具箱的 AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="fbb30-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="fbb30-119">使用 AJAX Control Toolkit 最簡單方式是將此工具組新增至您的 Visual Studio/Visual Web Developer 工具箱 （請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="fbb30-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="fbb30-120">這樣一來，您可以只將 toolkit 控制項拖曳至頁面時您想要使用它。</span><span class="sxs-lookup"><span data-stu-id="fbb30-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


<span data-ttu-id="fbb30-121">[![AJAX Control Toolkit 會出現在工具箱中](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fbb30-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="fbb30-122">**圖 03**:AJAX Control Toolkit 會出現在 [工具箱] ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="fbb30-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="fbb30-123">首先，您要新增至工具箱的 AJAX Control Toolkit 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fbb30-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="fbb30-124">請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fbb30-124">Follow these steps.</span></span>

1. <span data-ttu-id="fbb30-125">選取功能表選項的檔案，新的網站，以建立新的 ASP.NET 網站。</span><span class="sxs-lookup"><span data-stu-id="fbb30-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="fbb30-126">按兩下 [方案總管] 視窗中的 Default.aspx，在編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="fbb30-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="fbb30-127">以滑鼠右鍵按一下 一般 索引標籤下方的 工具箱，然後選取功能表選項**加入索引標籤**（請參閱 圖 4）。</span><span class="sxs-lookup"><span data-stu-id="fbb30-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="fbb30-128">輸入名為 AJAX Control Toolkit 中的新索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fbb30-128">Enter a new tab named AJAX Control Toolkit.</span></span>


<span data-ttu-id="fbb30-129">[![將新的索引標籤](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fbb30-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="fbb30-130">**圖 04**:將新的索引標籤 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="fbb30-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="fbb30-131">接下來，您需要將 AJAX Control Toolkit 控制項新增至新的索引標籤。請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fbb30-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="fbb30-132">以滑鼠右鍵按一下下方的 [AJAX Control Toolkit] 索引標籤，然後選取功能表選項**選擇的項目 （請參閱 [圖 5]）**。</span><span class="sxs-lookup"><span data-stu-id="fbb30-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="fbb30-133">瀏覽至您解壓縮 AJAX Control Toolkit 和選取 AjaxControlToolkit.dll 組件的位置。</span><span class="sxs-lookup"><span data-stu-id="fbb30-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


<span data-ttu-id="fbb30-134">[![選擇要加入至工具箱項目](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fbb30-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="fbb30-135">**圖 05**:選擇要加入至工具箱項目 ([按一下以檢視完整大小的影像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="fbb30-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="fbb30-136">完成這些步驟之後，所有的工具組控制項都會顯示在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="fbb30-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="fbb30-137">升級至新版本的工具組</span><span class="sxs-lookup"><span data-stu-id="fbb30-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="fbb30-138">如果您已使用的版本還舊的工具組，而且現在需要將移至較新的版本是建議的步驟：</span><span class="sxs-lookup"><span data-stu-id="fbb30-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="fbb30-139">二進位檔-從您網站的 Bin 資料夾刪除 AjaxControlToolkit.dll 組件的舊版本。</span><span class="sxs-lookup"><span data-stu-id="fbb30-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="fbb30-140">工具箱項目-刪除 AJAX Control Toolkit 索引標籤，並遵循上述步驟，以重新建立具有新版 AjaxControlToolkit.dll 組件的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fbb30-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fbb30-141">下一步</span><span class="sxs-lookup"><span data-stu-id="fbb30-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
