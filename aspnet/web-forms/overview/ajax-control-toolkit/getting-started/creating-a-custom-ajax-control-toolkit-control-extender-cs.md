---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: 建立自訂 AJAX 控制工具套件控制延伸器 (C#) |微軟文件
author: rick-anderson
description: 自訂擴充程式使您能夠自訂和擴展ASP.NET控件的功能,而無需創建新類。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ac7bf71227459ab4b1e87489e1faab6dc41545b
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543024"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>建立自訂的 AJAX Control Toolkit 控制項擴充項 (C#)

由[微軟](https://github.com/microsoft)

> 自訂擴充程式使您能夠自訂和擴展ASP.NET控件的功能,而無需創建新類。

在本教學中,您將瞭解如何創建自定義 AJAX 控制件工具套件控制元件延伸器。 我們創建一個簡單但有用的新擴展器,當您在 TextBox 中鍵入文本時,將按鈕的狀態從禁用更改為啟用。 閱讀本教程後,您將能夠使用自己的控制元件擴展器擴展ASP.NET AJAX 工具組。

您可以使用視覺化工作室或可視化 Web 開發人員建立自訂控制元件擴展器(請確保您具有最新版本的視覺化 Web 開發人員)。

## <a name="overview-of-the-disabledbutton-extender"></a>關閉按鈕延伸器概述

我們的新控制擴展器被命名為禁用按鈕擴展器。 新增延伸器將有三個屬性:

- 目標控制ID - 控制元件擴展的文字框。
- 目標ButtonIID - 已關閉或啟用的按鈕。
- 關閉文字 - 最初顯示在按鈕中的文字。 開始鍵入時,按鈕將顯示按鈕文本屬性的值。

將「禁用按鈕擴展器」掛到文字框和按鈕控制件。 鍵入任何文字之前,將禁用「按鈕」,文本框和按鈕如下所示:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png))

開始鍵入文字後,將啟用「按鈕」,文字框和按鈕如下所示:

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png))

要建立我們的控制器擴充器,我們需要建立以下三個檔案:

- DisabledButtonExtender.cs - 此檔案是伺服器端控制類,用於管理創建擴展器,並允許您在設計時設置屬性。 它還定義可以在擴展器上設置的屬性。 這些屬性可透過代碼和設計時間存取,並匹配在禁用ButtonBehavior.js檔中定義的屬性。
- 關閉ButtonBehavior.js -- 此檔案是您將添加所有用戶端文本邏輯的位置。
- DisabledButtonDesigner.cs - 此類啟用設計時功能。 如果希望控件擴展器與可視化工作室/可視化 Web 開發人員設計器正確工作,則需要此類。

因此,控制項裝置擴展器由伺服器端控制、用戶端行為和伺服器端設計器類組成。 您將在以下部分瞭解如何建立所有三個這些檔。

## <a name="creating-the-custom-extender-website-and-project"></a>建立自訂延伸器網站和專案

第一步是在可視化工作室/可視化 Web 開發人員中創建類庫專案和網站。 我們將在類庫項目中創建自定義擴展器,並在網站中測試自定義擴展器。

讓我們從網站開始。 依以下步驟建立網站:

1. 選擇選單選項 **「檔案,新建網站**」。
2. 選擇**ASP.NET 網站**樣本。
3. 命名新的*網站網站1。*
4. 按一下 [確定]**** 按鈕。

接下來,我們需要創建包含控制項擴展器代碼的類庫專案:

1. 選擇選單選項 **「檔、添加、新專案**」。
2. 選擇**類庫**範本。
3. 使用名稱 **「自訂擴充器**」為新類庫命名。
4. 按一下 [確定]**** 按鈕。

完成這些步驟後,解決方案資源管理器視窗應類似於圖 1。

[![網站和類別庫專案的解決方案](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**圖01:** 包含網站和類別庫專案的解決方案([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png))

接下來,您需要向類庫專案添加所有必要的程式集引用:

1. 右鍵按下「自訂擴展器」專案並選擇功能表選項 **「新增參考**」 。
2. 選取 [.NET] 索引標籤。
3. 加入下列組件的參考：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. 系統.Web.延伸.設計.dll
4. 選取 [瀏覽] 索引標籤。
5. 添加對 AjaxControlToolkit.dll 程式集的引用。 此程式集位於下載 AJAX 控制工具套件的資料夾中。

完成這些步驟后,類庫專案參考資料夾應類似於圖 2。

[![具有所需參考的參考資料夾](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**圖 02**:參考需要參考的資料夾([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png))

## <a name="creating-the-custom-control-extender"></a>建立自訂控制器

現在,我們已經有了類庫,我們可以開始構建擴展器控件。 讓我們從自定義擴展器控件類的裸骨開始(參見清單 1)。

**清單 1 - MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

關於清單1中的控件擴展器類,您注意到幾件事。 首先,請注意,類從基擴展器控制庫類繼承。 所有 AJAX 控制工具套件擴展器控制項都源自此基類。 例如,基類包括作為每個控制元件擴展器的必需屬性的 TargetID 屬性。

接下來,請注意,該類包含以下與用戶端腳本相關的兩個屬性:

- Web 資源 - 使檔案作為嵌入資源包含在程式集中。
- 用戶端文稿資源 - 導致從程式集檢索腳本資源。

WebResource 屬性用於在編譯自定義擴展器時將 MyControlBehavior.js JavaScript 檔嵌入到程式集中。 當在網頁中使用自定義擴展器時,用戶端腳本資源屬性用於從程式集中檢索 MyControlBehavior.js 文稿。

為了使 Web 資源和用戶端文本資源屬性正常工作,必須將 JavaScript 檔案編譯為嵌入式資源。 在解決方案資源管理器視窗中選擇檔,打開屬性表,並將值 *「嵌入資源」* 分配給 **「生成操作」** 屬性。

請注意,控制器還包括一個 TargetControlType 屬性。 此屬性用於指定由控制器擴展器擴展的控制項類型。 在清單 1 中,控制器用於擴展 TextBox。

最後,請注意,自定義擴展器包含名為 MyProperty 的屬性。 屬性使用擴展器控制屬性屬性進行標記。 GetPropertyValue() 和 SetPropertyValue() 方法用於將屬性值從伺服器端控制元件擴展器傳遞到客戶端行為。

讓我們繼續實現我們的禁用按鈕擴展器的代碼。 此擴展器的代碼可在清單 2 中找到。

**清單2 - DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

清單2中的"禁用按鈕擴展器"具有兩個屬性,分別命名為TargetButtonID和"禁用文本"。 應用於 TargetButtonID 屬性的 IDReference 屬性可防止您將 Button 控制項 ID 以外的任何內容分配給此屬性。

WebResource 和 ClientScriptResource 屬性將位於名為"禁用ButtonBehavior.js"的檔案中的客戶端行為與此擴展器相關聯。 我們將在下一節中討論此 JavaScript 檔。

## <a name="creating-the-custom-extender-behavior"></a>建立自訂延伸程式行為

控件擴展器的用戶端元件稱為行為。 關閉和啟用按鈕的實際邏輯包含在"禁用按鈕"行為中。 該行為的 JavaScript 代碼包含在清單 3 中。

**清單 3 - 停用Button.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

清單3中的 JavaScript 檔包含名為"禁用Button行為"的用戶端類。 此類,與其伺服器端孿生一樣,包括名為 TargetButtonID 和禁用文本的兩個屬性,您\_可以使用 GetTargetButtonID/設置\_TargetButtonID\_進行訪問,並獲得\_禁用文本/集 禁用文本。

初始化() 方法將鍵up事件處理程式與行為的目標元素關聯。 每次在與此行為關聯的 TextBox 中鍵入字母時,鍵 up 處理程序都會執行。 鍵up 處理程式啟用或禁用按鈕,具體取決於與該行為關聯的 TextBox 是否包含任何文本。

請記住,您必須將清單 3 中的 JavaScript 檔編譯為嵌入式資源。 在解決方案資源管理器視窗中選擇檔,打開屬性表,並將值 *「嵌入資源」* 分配給**生成操作**屬性(參見圖 3)。 此選項在可視化工作室和可視化 Web 開發人員中都可用。

[![將 JavaScript 檔案加入為嵌入式資源](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**圖 03**: 將 JavaScript 檔案加入為嵌入式資源([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png))

## <a name="creating-the-custom-extender-designer"></a>建立自訂延伸程式設計器

我們需要創建最後一個類來完成擴展器。 我們需要在清單4中創建設計器類。 此類是使擴展器在可視化工作室/可視化 Web 開發人員設計器中正確運行所必需的。

**清單4 - DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

將清單 4 中的設計器與「已禁用Button擴展器」與「設計器」屬性相關聯。您需要將 Designer 屬性應用於禁用Button擴展器類,如下所示:

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>使用自訂延伸器

現在,我們已經完成了創建禁用按鈕控件擴展器,是時候在我們的ASP.NET網站使用它了。 首先,我們需要將自定義擴展器添加到工具箱中。 請遵循下列步驟：

1. 通過按兩下解決方案資源管理器視窗中的頁面打開ASP.NET頁。
2. 右鍵按一下工具箱並選擇選單選項 **「選擇專案**」。
3. 在「選擇工具箱項目」對話框中,流覽到「自訂擴展器.dll」程式集。
4. 按下「**確定」** 按鈕關閉對話方塊。

完成這些步驟後,禁用 Button 控件擴展器應顯示在工具箱中(參見圖 4)。

[![工具箱中的關閉按鈕](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**圖 04**: 工具殼中的關閉按鈕([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png))

接下來,我們需要創建一個新的ASP.NET頁。 請遵循下列步驟：

1. 創建新ASP.NET頁面名為"顯示禁用按鈕.aspx"。
2. 將腳本管理器拖到頁面上。
3. 將文字框控件拖到頁面上。
4. 將「按鈕」控制器拖到頁面上。
5. 在"屬性"視窗中,將按鈕ID屬性更改為值<em>btnSave,</em>將文本屬性更改為*\*值"儲存*"。

我們創建了一個包含標準ASP.NET文本框和按鈕控制項的頁面。

接下來,我們需要使用關閉按鈕延伸器延伸 TextBox 控制件:

1. 選擇 **「新增延伸器**」工作選項以開啟延伸程式精靈對話框(參見圖 5)。 請注意,該對話框包括我們的自定義禁用按鈕擴展器。
2. 選擇"停用按鈕擴展器",然後按下 **「確定**」按鈕。

[![擴充器精靈對話框](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**圖 05**: 擴充器精靈對話框([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png))

最後,我們可以設置禁用按鈕擴展器的屬性。 您可以透過修改 TextBox 控制檔屬性來變更關閉Button延伸器的屬性:

1. 選擇設計器中的文字框。
2. 在"屬性"視窗中,展開擴展器節點(參見圖 6)。
3. 將「*儲存到*關閉文字」 屬性的值和值*btnSave*分配給 TargetButtonID 屬性。

[![設定延伸器屬性](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**圖 06**:設定延伸器屬性([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png))

當您運行頁面(通過點擊 F5)時,按鈕控制項最初被禁用。 一旦您開始將文字輸入到 TextBox 中,按鈕控制件即啟用(參見圖 7)。

[![關閉按鈕延伸器正在操作中](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**圖 07**: 關閉按鈕延伸器在操作中([按下以檢視全尺寸影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png))

## <a name="summary"></a>總結

本教學的目的是說明如何使用自定義擴展器控制項擴展 AJAX 控制項工具組。 在本教學中,我們創建了一個簡單的禁用按鈕控制元件擴展器。 我們通過創建禁用Button擴展器類、禁用Button行為 JavaScript 行為和禁用ButtonDesigner類實現了此擴展程式。 每當創建自定義控制器時,都會遵循一組類似的步驟。

> [!div class="step-by-step"]
> [前一個](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
> [下一個](get-started-with-the-ajax-control-toolkit-vb.md)
