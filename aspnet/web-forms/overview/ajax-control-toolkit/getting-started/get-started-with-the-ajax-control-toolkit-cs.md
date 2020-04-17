---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 開始使用 AJAX 控制工具套件 (C#) |微軟文件
author: rick-anderson
description: 了解開始使用 AJAX 控制工具套件所需的所有知識。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: b5954019ec3312f06f38012e4d3f9b1f71573f76
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543583"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="02cc7-103">開始使用 AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="02cc7-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="02cc7-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="02cc7-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="02cc7-105">了解開始使用 AJAX 控制工具套件所需的所有知識。</span><span class="sxs-lookup"><span data-stu-id="02cc7-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="02cc7-106">AJAX 控制工具組包含 30 多個免費控制項,可用於ASP.NET應用程式中。</span><span class="sxs-lookup"><span data-stu-id="02cc7-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="02cc7-107">在本教學中,您將瞭解如何下載 AJAX 控制件工具組,並將工具套件控制項添加到可視化工作室/視覺化 Web 開發人員快速工具箱。</span><span class="sxs-lookup"><span data-stu-id="02cc7-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="02cc7-108">下載 AJAX 控制工具套件</span><span class="sxs-lookup"><span data-stu-id="02cc7-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="02cc7-109">[AJAX 控制工具套件](http://devexpress.com/act)是由ASP.NET社區成員和ASP.NET團隊開發的開源專案。</span><span class="sxs-lookup"><span data-stu-id="02cc7-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="02cc7-110">[![下載 AJAX 控制工具套件](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="02cc7-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="02cc7-111">**圖 01**: 下載 AJAX 控制工具套件([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="02cc7-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="02cc7-112">下載檔后,需要取消阻止該檔。</span><span class="sxs-lookup"><span data-stu-id="02cc7-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="02cc7-113">右鍵按一下檔案,選擇「屬性」,然後按下 **「取消阻止」** 按鈕(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="02cc7-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="02cc7-114">[![取消封鎖 AJAX 控制工具套件 ZIP 檔案](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="02cc7-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="02cc7-115">**圖 02**: 取消封鎖 AJAX 控制工具套件 ZIP 檔案([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="02cc7-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="02cc7-116">取消阻止檔案後,可以解壓縮檔:右鍵單擊該檔並選擇 **「全部提取」** 選單選項。</span><span class="sxs-lookup"><span data-stu-id="02cc7-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="02cc7-117">現在,我們準備將工具組添加到可視化工作室/可視化 Web 開發人員工具箱。</span><span class="sxs-lookup"><span data-stu-id="02cc7-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="02cc7-118">將 AJAX 控制工具套件加入工具箱</span><span class="sxs-lookup"><span data-stu-id="02cc7-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="02cc7-119">使用 AJAX 控制工具套件的最簡單方法是將工具組添加到可視化工作室/可視化 Web 開發人員工具箱(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="02cc7-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="02cc7-120">這樣,您只需在要使用工具組控制程式時將其拖到頁面上即可。</span><span class="sxs-lookup"><span data-stu-id="02cc7-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="02cc7-121">[![AJAX 控制工具套件顯示在工具箱中](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="02cc7-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="02cc7-122">**圖 03**: AJAX 控制工具套件顯示在工具箱中([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="02cc7-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="02cc7-123">首先,您需要向工具箱添加 AJAX 控制工具套件選項卡。</span><span class="sxs-lookup"><span data-stu-id="02cc7-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="02cc7-124">請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="02cc7-124">Follow these steps.</span></span>

1. <span data-ttu-id="02cc7-125">通過選擇功能表選項「檔,新網站」,創建新ASP.NET網站。</span><span class="sxs-lookup"><span data-stu-id="02cc7-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="02cc7-126">按兩下解決方案資源管理器視窗中的 Default.aspx 以在編輯器中打開該檔。</span><span class="sxs-lookup"><span data-stu-id="02cc7-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="02cc7-127">右鍵按下「常規選項卡」下方的工具框,然後選擇功能表選項 **「添加選項卡**」(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="02cc7-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="02cc7-128">輸入名為 AJAX 控制工具套件的新選項卡。</span><span class="sxs-lookup"><span data-stu-id="02cc7-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="02cc7-129">[![新增選項卡](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="02cc7-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="02cc7-130">**圖 04**:新增新選項卡([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="02cc7-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="02cc7-131">接下來,您需要將 AJAX 控制項工具套件控制項加入新選項卡中。按照以下步驟操作:</span><span class="sxs-lookup"><span data-stu-id="02cc7-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="02cc7-132">右鍵單擊 AJAX 控制工具組選項卡下方,然後選擇功能表選項 **「選擇專案」(參見圖 5)。**</span><span class="sxs-lookup"><span data-stu-id="02cc7-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="02cc7-133">瀏覽到解壓縮 AJAX 控制工具套件的位置,然後選擇 AjaxControlToolkit.dll 程式集。</span><span class="sxs-lookup"><span data-stu-id="02cc7-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="02cc7-134">[![選擇要新增到工具箱的項目](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="02cc7-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="02cc7-135">**圖 05**: 選擇要加入工具箱的項目([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="02cc7-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="02cc7-136">完成這些步驟后,所有工具組控制者都將顯示在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="02cc7-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="02cc7-137">升級到新版本的工具組</span><span class="sxs-lookup"><span data-stu-id="02cc7-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="02cc7-138">如果您使用的是舊版本的工具組,現在需要移動到更高版本,下面是建議的步驟:</span><span class="sxs-lookup"><span data-stu-id="02cc7-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="02cc7-139">二進位 - 從您的網站 Bin 資料夾中刪除 AjaxControlToolkit.dll 程式集的舊版本。</span><span class="sxs-lookup"><span data-stu-id="02cc7-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="02cc7-140">工具箱專案 - 刪除 AJAX 控制工具組選項卡,然後按照上述步驟重新建立具有新版本 AjaxControlToolkit.dll 程式集的選項卡。</span><span class="sxs-lookup"><span data-stu-id="02cc7-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="02cc7-141">下一步</span><span class="sxs-lookup"><span data-stu-id="02cc7-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
