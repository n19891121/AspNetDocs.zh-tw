---
uid: web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
title: '建立自訂的 AJAX 控制項工具組控制項擴充項 (c # ) |Microsoft Docs'
author: rick-anderson
description: 自訂擴充項可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 96b56eca-a892-45a4-96b4-67e61178650a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/creating-a-custom-ajax-control-toolkit-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 2522f22c80ebd34cd5adbb0ada51fd7755029426
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89044660"
---
# <a name="creating-a-custom-ajax-control-toolkit-control-extender-c"></a>建立自訂的 AJAX Control Toolkit 控制項擴充項 (C#)

由 [Microsoft](https://github.com/microsoft)

> 自訂擴充項可讓您自訂和擴充 ASP.NET 控制項的功能，而不需要建立新的類別。

在本教學課程中，您將瞭解如何建立自訂的 AJAX 控制項工具組控制項擴充項。 我們會建立一個簡單但有用的新擴充項，在您將文字輸入文字方塊時，將按鈕的狀態從停用變更為啟用。 閱讀本教學課程之後，您將能夠使用自己的控制項擴充項來擴充 ASP.NET AJAX 工具組。

您可以使用 Visual Studio 或 Visual Web Developer 來建立自訂控制項擴充項 (確定您有最新版本的 Visual Web Developer) 。

## <a name="overview-of-the-disabledbutton-extender"></a>DisabledButton 擴充項的總覽

我們的新控制項擴充項會命名為 DisabledButton 擴充項。 此擴充項會有三個屬性：

- TargetControlID-控制項所擴充的 TextBox。
- TargetButtonIID-已停用或已啟用的按鈕。
- DisabledText-一開始在按鈕中顯示的文字。 當您開始輸入時，按鈕會顯示按鈕 Text 屬性的值。

您將 DisabledButton 擴充項鍊接至 TextBox 和 Button 控制項。 輸入任何文字之前，按鈕會停用，且 TextBox 和 Button 看起來像這樣：

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image2.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image1.png)

 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image3.png)) 

當您開始輸入文字之後，按鈕就會啟用，而且 TextBox 和 Button 看起來像這樣：

[![](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image5.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image4.png)

 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image6.png)) 

若要建立控制項擴充項，我們需要建立下列三個檔案：

- DisabledButtonExtender.cs-此檔案是伺服器端控制項類別，可管理您的擴充項建立，並可讓您在設計階段設定屬性。 它也會定義可在擴充項上設定的屬性。 這些屬性可透過程式碼和在設計階段存取，並符合 DisableButtonBehavior.js 檔中定義的屬性。
- DisabledButtonBehavior.js--這個檔案是您將加入所有用戶端腳本邏輯的位置。
- DisabledButtonDesigner.cs-這個類別可啟用設計階段功能。 如果您想要讓控制項擴充項正確地使用 Visual Studio/Visual Web Developer Designer，您需要這個類別。

因此，控制項擴充項是由伺服器端控制項、用戶端行為，以及伺服器端設計工具類別所組成。 您將在下列各節中瞭解如何建立這三個檔案。

## <a name="creating-the-custom-extender-website-and-project"></a>建立自訂擴充項網站和專案

第一個步驟是在 Visual Studio/Visual Web Developer 中建立類別庫專案和網站。 我們將在類別庫專案中建立自訂擴充項，並在網站中測試自訂擴充項。

讓我們從網站開始。 遵循下列步驟來建立網站：

1. 選取功能表選項 [檔案] **、[新增網站**]。
2. 選取 [ **ASP.NET] 網站** 範本。
3. 將新網站命名為 *Website1*。
4. 按一下 [確定] 按鈕。

接下來，我們需要建立將包含控制項擴充項程式碼的類別庫專案：

1. 選取功能表選項 [檔案] **、[加入]、[新增專案**]。
2. 選取 [ **類別庫** ] 範本。
3. 以名稱 **CustomExtenders**命名新的類別庫。
4. 按一下 [確定] 按鈕。

完成這些步驟之後，您的方案總管視窗看起來應該如圖1所示。

[![具有網站和類別庫專案的解決方案](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image8.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image7.png)

**圖 01**：包含網站和類別庫專案的方案 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image9.png)) 

接下來，您必須將所有必要的元件參考加入至類別庫專案：

1. 以滑鼠右鍵按一下 [CustomExtenders] 專案，然後選取 [ **加入參考**] 功能表選項。
2. 選取 [.NET] 索引標籤。
3. 加入下列組件的參考：

    1. System.Web.dll
    2. System.Web.Extensions.dll
    3. System.Design.dll
    4. System.Web.Extensions.Design.dll
4. 選取 [瀏覽] 索引標籤。
5. 加入 AjaxControlToolkit.dll 元件的參考。 這個元件位於您下載 AJAX 控制項工具組的資料夾中。

完成這些步驟之後，您的類別庫專案參考資料夾看起來應該如圖2所示。

[![具有必要參考的參考資料夾](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image11.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image10.png)

**圖 02**：參考具有必要參考的資料夾 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image12.png)) 

## <a name="creating-the-custom-control-extender"></a>建立自訂控制項擴充項

既然我們有了類別庫，就可以開始建立我們的擴充項控制項。 讓我們從自訂擴充項控制項類別的裸機開始 (請參閱 [清單 1]) 。

**清單 1-MyCustomExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample1.cs)]

您會在 [清單 1] 中看到關於控制項擴充項類別的幾件事。 首先，請注意，此類別繼承自基底 ExtenderControlBase 類別。 所有 AJAX 控制項工具組的擴充性控制項都是衍生自這個基類。 例如，基類包含 TargetID 屬性，這是每個控制項擴充項的必要屬性。

接下來，請注意類別包含下列兩個與用戶端腳本相關的屬性：

- WebResource-導致檔案以內嵌資源的形式包含在元件中。
- ClientScriptResource：讓腳本資源從元件中取出。

WebResource 屬性是用來在編譯自訂擴充項時，將 MyControlBehavior.js 的 JavaScript 檔案內嵌至元件。 當自訂擴充項用於網頁時，ClientScriptResource 屬性會用來從元件中取出 MyControlBehavior.js 腳本。

為了讓 WebResource 和 ClientScriptResource 屬性能夠運作，您必須將 JavaScript 檔案編譯為內嵌資源。 在 [方案總管] 視窗中選取檔案，開啟屬性工作表，然後將值 *內嵌資源* 指派給 [ **組建動作** ] 屬性。

請注意，控制項擴充項也包含 TargetControlType 屬性。 這個屬性是用來指定控制項擴充項所擴充的控制項型別。 在 [清單 1] 的案例中，會使用控制項擴充項來擴充 TextBox。

最後，請注意，自訂擴充項包含名為 MyProperty 的屬性。 屬性會以 ExtenderControlProperty 屬性標記。 GetPropertyValue ( # A1 和 SetPropertyValue ( # A3 方法可用來將屬性值從伺服器端控制項擴充項傳遞至用戶端行為。

讓我們繼續執行 DisabledButton 擴充項的程式碼。 此擴充項的程式碼可在 [清單 2] 中找到。

**清單 2-DisabledButtonExtender.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample2.cs)]

[清單 2] 中的 DisabledButton 擴充項具有兩個名為 TargetButtonID 和 DisabledText 的屬性。 套用至 TargetButtonID 屬性的 IDReferenceProperty 可防止您將 Button 控制項的 ID 以外的任何內容指派給這個屬性。

WebResource 和 ClientScriptResource 屬性會將位於名為 DisabledButtonBehavior.js 之檔案中的用戶端行為與此擴充項產生關聯。 我們將在下一節討論這個 JavaScript 檔案。

## <a name="creating-the-custom-extender-behavior"></a>建立自訂擴充項行為

控制項擴充項的用戶端元件稱為行為。 停用和啟用按鈕的實際邏輯都包含在 DisabledButton 行為中。 此行為的 JavaScript 程式碼會包含在 [清單 3] 中。

**清單 3-DisabledButton.js**

[!code-javascript[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample3.js)]

[清單 3] 中的 JavaScript 檔案包含名為 DisabledButtonBehavior 的用戶端類別。 這個類別（例如其伺服器端對應項）包含兩個名為 TargetButtonID 和 DisabledText 的屬性，您可以使用 get \_ TargetButtonID/set \_ TargetButtonID 和 get \_ DisabledText/set DisabledText 來存取這些屬性 \_ 。

Initialize ( # A1 方法會將 keyup 事件處理常式與行為的目標元素產生關聯。 每次您在與此行為相關聯的文字方塊中輸入字母時，就會執行 keyup 處理常式。 Keyup 處理常式會根據與行為相關聯的文字方塊是否包含任何文字，來啟用或停用按鈕。

請記住，您必須在 [清單 3] 中將 JavaScript 檔案編譯為內嵌資源。 在 [方案總管] 視窗中選取檔案，開啟屬性工作表，並將 [ *內嵌資源* ] 值指派給 [ **組建動作** ] 屬性 (請參閱 [圖 3]) 。 Visual Studio 和 Visual Web Developer 都有提供這個選項。

[![將 JavaScript 檔案新增為內嵌資源](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image14.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image13.png)

**圖 03**：將 JavaScript 檔案新增為內嵌資源 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image15.png)) 

## <a name="creating-the-custom-extender-designer"></a>建立自訂擴充項設計工具

最後一個類別需要建立，才能完成我們的擴充項。 我們需要建立 [清單 4] 中的設計工具類別。 此類別是讓擴充項使用 Visual Studio/Visual Web Developer Designer 正確運作的必要類別。

**清單 4-DisabledButtonDesigner.cs**

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample4.cs)]

您可以使用設計工具屬性，將 [清單 4] 中的設計工具與 DisabledButton 擴充項產生關聯。您必須將設計工具屬性套用至 DisabledButtonExtender 類別，如下所示：

[!code-csharp[Main](creating-a-custom-ajax-control-toolkit-control-extender-cs/samples/sample5.cs)]

## <a name="using-the-custom-extender"></a>使用自訂擴充項

既然我們已完成建立 DisabledButton 控制項擴充項，現在就可以在我們的 ASP.NET 網站中使用它。 首先，我們需要將自訂擴充項加入至 [工具箱]。 請遵循下列步驟：

1. 按兩下方案總管視窗中的頁面，即可開啟 ASP.NET 網頁。
2. 以滑鼠右鍵按一下 [工具箱]，然後選取功能表選項 [ **選擇專案**]。
3. 在 [選擇工具箱專案] 對話方塊中，流覽至 CustomExtenders.dll 元件。
4. 按一下 [ **確定** ] 按鈕以關閉對話方塊。

完成這些步驟之後，[DisabledButton] 控制項擴充項應該會出現在 [工具箱] 中 (請參閱 [圖 4]) 。

[![工具箱中的 DisabledButton](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image17.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image16.png)

**圖 04**：在 [工具箱] 中 DisabledButton ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image18.png)) 

接下來，我們需要建立新的 ASP.NET 網頁。 請遵循下列步驟：

1. 建立新的 ASP.NET 網頁，名為 ShowDisabledButton .aspx。
2. 將 ScriptManager 拖曳到頁面上。
3. 將 TextBox 控制項拖曳至頁面上。
4. 將按鈕控制項拖曳至頁面上。
5. 在 [屬性視窗中，將 [按鈕識別碼] 屬性變更為 [值<em>btnSave</em> ]，並將 [Text] 屬性變更為 [*儲存 \* *]。

我們建立了具有標準 ASP.NET TextBox 和 Button 控制項的頁面。

接下來，我們需要使用 DisabledButton 擴充項來擴充 TextBox 控制項：

1. 選取 [ **加入** 擴充項工作] 選項以開啟 [擴充項 Wizard] 對話方塊 (參閱 [圖 5]) 。 請注意，此對話方塊包含我們的自訂 DisabledButton 擴充項。
2. 選取 DisabledButton 擴充項，然後按一下 [ **確定]** 按鈕。

[![[擴充項 Wizard] 對話方塊](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image20.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image19.png)

**圖 05**：擴充項 Wizard 對話方塊 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image21.png)) 

最後，我們可以設定 DisabledButton 擴充項的屬性。 您可以藉由修改 TextBox 控制項的屬性來修改 DisabledButton 擴充項的屬性：

1. 選取設計工具中的文字方塊。
2. 在屬性視窗中，展開 [擴充項] 節點 (請參閱圖 6) 。
3. 將值 *Save* 指派給 DisabledText 屬性，並將值 *BtnSave* 指派給 TargetButtonID 屬性。

[![設定擴充項屬性](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image23.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image22.png)

**圖 06**：設定擴充項屬性 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image24.png)) 

當您按下 F5)  (執行頁面時，按鈕控制項會一開始停用。 一旦您開始在文字方塊中輸入文字，就會啟用按鈕控制項 (請參閱 [圖 7]) 。

[![作用中的 DisabledButton 擴充項](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image26.png)](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image25.png)

**圖 07**： DisabledButton 擴充項的作用 ([按一下以查看完整大小的影像](creating-a-custom-ajax-control-toolkit-control-extender-cs/_static/image27.png)) 

## <a name="summary"></a>總結

本教學課程的目的是要說明如何使用自訂擴充項控制項來擴充 AJAX 控制項工具組。 在本教學課程中，我們建立了簡單的 DisabledButton 控制項擴充項。 我們藉由建立 DisabledButtonExtender 類別、DisabledButtonBehavior JavaScript 行為和 DisabledButtonDesigner 類別，來實作為擴充項。 當您建立自訂控制項擴充項時，您可以遵循一組類似的步驟。

> [!div class="step-by-step"]
> [上一個](using-ajax-control-toolkit-controls-and-control-extenders-cs.md) 
> [下一步](get-started-with-the-ajax-control-toolkit-vb.md)
