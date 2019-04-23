---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 建立控制器 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: c92d7cdeb7b2d31d5eca810628e9f563840f7494
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59400598"
---
# <a name="creating-a-controller-c"></a>建立控制器 (C#)

藉由[Stephen Walther](https://github.com/StephenWalther)

> 在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。


本教學課程的目標是要說明如何建立新的 ASP.NET MVC 控制站。 您了解如何建立控制站，藉由使用 Visual Studio [新增控制器] 功能表選項，以及藉由以手動方式建立的類別檔案。

### <a name="using-the-add-controller-menu-option"></a>使用 [新增控制器] 功能表選項

若要建立新的控制站的最簡單方式是在 Visual Studio 方案總管] 視窗中的 [控制器] 資料夾上按一下滑鼠右鍵，然後選取**新增]、 [控制站**功能表選項 （請參閱 [圖 1）。 選取此功能表選項會開啟**新增控制器**對話方塊 （請參閱 圖 2）。


[![[新增專案] 對話方塊](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)

**圖 01**:加入新的控制站 ([按一下以檢視完整大小的影像](creating-a-controller-cs/_static/image2.png))


[![[新增專案] 對話方塊](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)

**圖 02**:[新增控制器] 對話方塊 ([按一下以檢視完整大小的影像](creating-a-controller-cs/_static/image4.png))


請注意，控制器名稱的第一個部分會以醒目提示**新增控制器**對話方塊。 每個控制站名稱必須以尾碼結尾*控制器*。 比方說，您可以在其中建立名為控制器*ProductController*但不是將名為控制器*產品*。


如果您建立遺漏的控制站*控制器*後置詞，則您將無法叫用控制器。 千萬不要這麼做，我已浪費許多時間進行這種錯誤後我的生活。


**Listing 1 - Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

您應該在 Controllers 資料夾中建立控制站。 否則，會違反您的 ASP.NET MVC 慣例，而且其他開發人員會有更難了解您的應用程式。

### <a name="scaffolding-action-methods"></a>Scaffolding 動作方法

當您建立一個控制站時，您可以選擇自動產生 Create、 Update 和詳細資料的動作方法 （請參閱 [圖 3]）。 如果您選取此選項則會產生列表 2 中的控制器類別。


[![自動建立動作方法](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)

**圖 03**:自動建立動作方法 ([按一下以檢視完整大小的影像](creating-a-controller-cs/_static/image6.png))


**列表 2-Controllers\CustomerController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

這些產生的方法是虛設常式方法。 您必須新增建立、 更新和顯示詳細資料的客戶自己的實際邏輯。 但是，虛設常式方法會將您提供不錯的起點。

### <a name="creating-a-controller-class"></a>建立控制器類別

ASP.NET MVC 控制器是只是一個類別。 如果您想，您可以略過方便的 Visual Studio 控制器 scaffolding，並以手動方式建立控制器類別。 請依照下列步驟：

1. 以滑鼠右鍵按一下 控制器 資料夾，然後選取功能表選項**新增、 新項目**，然後選取**類別**範本 （請參閱 圖 4）。
2. 新的類別 PersonController.cs 命名，然後按一下**新增** 按鈕。
3. 修改產生的類別檔案，讓類別繼承自基底 system.web.mvc.controller 衍生類別 （請參閱列表 3）。


[![建立新的類別](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)

**圖 04**:建立新的類別 ([按一下以檢視完整大小的影像](creating-a-controller-cs/_static/image8.png))


**Listing 3 - Controllers\PersonController.cs**

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

列表 3 中的控制站會公開一個名為 index （） 會傳回字串"Hello World ！"的動作。 您可以叫用此控制器動作，以執行您的應用程式，並要求的 URL，如下所示：

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET Development Server 會使用隨機的連接埠號碼 (例如 40071)。 輸入時要叫用控制器的 URL，您必須提供正確的連接埠號碼。 您可以將滑鼠停留在圖示，ASP.NET 程式開發伺服器在 Windows 通知區域 （右下方的您的畫面），來判斷連接埠號碼。
> 
> [!div class="step-by-step"]
> [上一頁](adding-dynamic-content-to-a-cached-page-cs.md)
> [下一頁](creating-an-action-cs.md)
