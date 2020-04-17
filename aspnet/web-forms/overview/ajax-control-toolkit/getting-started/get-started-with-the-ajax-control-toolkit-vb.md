---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: 開始使用 AJAX 控制工具套件 (VB) |微軟文件
author: rick-anderson
description: 了解開始使用 AJAX 控制工具套件所需的所有知識。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: 6af5e293a35ce3e3ba35a0f7abfd2d92d538c84c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543557"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>開始使用 AJAX Control Toolkit (VB)

由[微軟](https://github.com/microsoft)

> 了解開始使用 AJAX 控制工具套件所需的所有知識。

AJAX 控制工具組包含 30 多個免費控制項,可用於ASP.NET應用程式中。 在本教學中,您將瞭解如何下載 AJAX 控制件工具組,並將工具套件控制項添加到可視化工作室/視覺化 Web 開發人員快速工具箱。

## <a name="downloading-the-ajax-control-toolkit"></a>下載 AJAX 控制工具套件

[AJAX 控制工具套件](http://devexpress.com/act)是由ASP.NET社區成員和ASP.NET團隊開發的開源專案。

[![下載 AJAX 控制工具套件](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**圖 01**: 下載 AJAX 控制工具套件([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

下載檔后,需要取消阻止該檔。 右鍵按一下檔案,選擇「屬性」,然後按下 **「取消阻止」** 按鈕(參見圖 2)。

[![取消封鎖 AJAX 控制工具套件 ZIP 檔案](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**圖 02**: 取消封鎖 AJAX 控制工具套件 ZIP 檔案([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

取消阻止檔案後,可以解壓縮檔:右鍵單擊該檔並選擇 **「全部提取」** 選單選項。 現在,我們準備將工具組添加到可視化工作室/可視化 Web 開發人員工具箱。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>將 AJAX 控制工具套件加入工具箱

使用 AJAX 控制工具套件的最簡單方法是將工具組添加到可視化工作室/可視化 Web 開發人員工具箱(參見圖 3)。 這樣,您只需在要使用工具組控制程式時將其拖到頁面上即可。

[![AJAX 控制工具套件顯示在工具箱中](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**圖 03**: AJAX 控制工具套件顯示在工具箱中([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))

首先,您需要向工具箱添加 AJAX 控制工具套件選項卡。 請遵循下列步驟。

1. 通過選擇功能表選項「檔,新網站」,創建新ASP.NET網站。 按兩下解決方案資源管理器視窗中的 Default.aspx 以在編輯器中打開該檔。
2. 右鍵按下「常規選項卡」下方的工具框,然後選擇功能表選項 **「添加選項卡**」(參見圖 4)。
3. 輸入名為 AJAX 控制工具套件的新選項卡。

[![新增選項卡](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**圖 04**:新增新選項卡([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

接下來,您需要將 AJAX 控制項工具套件控制項加入新選項卡中。按照以下步驟操作:

- 右鍵單擊 AJAX 控制工具組選項卡下方,然後選擇功能表選項 **「選擇專案」(參見圖 5)。**
- 瀏覽到解壓縮 AJAX 控制工具套件的位置,然後選擇 AjaxControlToolkit.dll 程式集。

[![選擇要新增到工具箱的項目](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**圖 05**: 選擇要加入工具箱的項目([按下以檢視全尺寸影像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))

完成這些步驟后,所有工具組控制者都將顯示在工具箱中。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>升級到新版本的工具組

如果您使用的是舊版本的工具組,現在需要移動到更高版本,下面是建議的步驟:

- 二進位 - 從您的網站 Bin 資料夾中刪除 AjaxControlToolkit.dll 程式集的舊版本。
- 工具箱專案 - 刪除 AJAX 控制工具組選項卡,然後按照上述步驟重新建立具有新版本 AjaxControlToolkit.dll 程式集的選項卡。

> [!div class="step-by-step"]
> [前一個](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一個](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
