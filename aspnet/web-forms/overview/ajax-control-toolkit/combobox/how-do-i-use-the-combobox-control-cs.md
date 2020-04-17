---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: 如何使用組合盒控件? (C#) |微軟文件
author: rick-anderson
description: ComboBox 是一ASP.NET AJAX 控制項,它將TextBox的靈活性與使用者可以選擇的選項清單相結合。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2adb9663cb7bdc38f28a127f7932f45a3447d1de
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543801"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>如何使用組合盒控件? (C#)

由[微軟](https://github.com/microsoft)

> ComboBox 是一ASP.NET AJAX 控制項,它將TextBox的靈活性與使用者可以選擇的選項清單相結合。

本教學的目的是解釋 AJAX 控制工具組組合盒控制件。 組合框的工作方式類似於標準ASP.NET下拉清單控制項和文字框控制元件之間的組合。 您可以從預先存在的項目清單中選擇,也可以輸入新專案。

組合盒類似於自動完成控制器擴充器,但控制項在不同的方案中使用。 自動完成擴展程序查詢 Web 服務以獲取匹配的條目。 相反,組合框控制項使用一組項進行初始化。 使用 AutoComplete 擴充程式在使用大量資料(數百萬個汽車零件)時有意義,而使用 ComboBox 控制件在使用一小組數據(數十個汽車部件)時是有意義的。

## <a name="selecting-from-a-static-list-of-items"></a>從靜態項目清單中選擇

讓我們從使用組合框控件的簡單示例開始。 假設您要在下拉清單中顯示項目的靜態清單。 但是,您希望保留清單未完成的可能性。 您希望允許使用者在清單中輸入自定義值。

我們將創建一個新的ASP.NET Web 窗體頁,並在該頁中使用 ComboBox 控件。 將新的ASP.NET頁添加到專案中並切換到"設計"視圖。

如果要在頁面中使用 ComboBox 控制項,則必須向頁面添加文本管理器控制項。 將文稿管理器控制項從 AJAX 延伸選項卡下方拖曳到設計器表面。 應在頁面頂部添加腳本管理器控件;但是,在頁面頂部,應添加腳本管理器控件。可以將其添加到打開的伺服器端&lt;窗&gt;體 標記的下方。

接下來,將組合框控件拖到頁面上。 您可以在工具箱中找到與其他 AJAX 控制工具套件控制器和控制擴展器一起的 ComboBox 控制件(見圖 1)。

[![建立名片的簡單表單](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**圖 01**: 從工具匣中選擇群組([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image2.png))

我們將使用組合框控件來顯示靜態選項清單。 用戶可以從三個選項清單中為其食物選擇特定級別的辣度(參見圖 2)。

[![從靜態項目清單中選擇](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**圖 02**:從靜態項目清單中選擇([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image4.png))

有兩種方法可以將這些選項添加到 ComboBox 控制件。 首先,在"設計"檢視中將滑鼠懸停在控制項上並打開專案編輯器時,請選擇"編輯選項"任務選項(參見圖 3)。

[![編輯組合框項目](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**圖 03**: 編輯組合盒項目([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image6.png))

第二個選項是在源檢視中的開盤和關閉&lt;asp:ComboBox&gt;標記之間添加專案清單。 清單 1 中的頁面包含包含專案清單的更新的 ComboBox。

**清單 1 - 靜態.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

在清單 1 中開啟頁面時,您可以從組合框中選擇一個預先存在的選項。 換句話說,組合框的工作方式與下拉清單控件類似。

但是,您還可以選擇輸入不在現有清單中的新選項(例如,超級辣)。 因此,組合框也像文本框控件一樣工作。

無論您選擇預先存在的項目還是輸入自定義專案,在提交表單時,您的選擇都會顯示在標籤控制項中。 提交表單時,btnSubmit\_單擊處理程式將執行並更新標籤(參見圖 4)。

[![顯示選取的項目](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**圖 04**:顯示選取的項目([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image8.png))

ComboBox 支援與提交表單後檢索選取的下拉清單控制件相同的屬性:

- 選定項目.文字 - 顯示選取的項目的文字屬性的值。
- 選定項目.值 - 顯示選取項目的值屬性的值或顯示鍵入到組合盒中的文字。
- 選取值 - 與選擇的項目相同。除非此屬性允許您指定預設(初始)選定專案。

如果在組合框中鍵入自定義選項,則自定義選項將分配給"選定專案.文本"和"選定專案"值屬性。

## <a name="selecting-the-list-of-items-from-the-database"></a>從資料庫中選擇項目清單

您可以檢索 ComboBox 從資料庫中顯示的專案清單。 例如,您可以將組合盒綁定到 SqlDataSource 控制項、ObjectDataSource 控制項、LinqDataSource 或實體資料來源。

假設您要在組合盒中顯示電影清單。 您希望從「影片」資料庫表中檢索影片清單。 請遵循下列步驟：

1. 建立名為「電影.aspx」的頁面
2. 通過將文稿管理器從工具箱中的 AJAX 擴展選項卡下拖動到頁面,將文本管理器控制項添加到頁面。
3. 通過將組合框拖到頁面上,將組合框控件添加到頁面。
4. 在"設計"檢視中,將滑鼠懸停在 ComboBox 控件上,然後選擇 **「選擇資料源**任務」選項(參見圖 5)。 啟動數據源配置嚮導。
5. 在**選擇資料來源**「步驟中,選擇」&lt;新的資料來源&gt;選項。
6. 在 **「選擇資料源類型」步驟中**,選擇「資料庫」。
7. 在 **「選擇數據連接**」步驟中,選擇資料庫(例如,MoviesDB.mdf)。
8. 在 **「將連接字串儲存到應用程式設定檔」步驟中**,選擇儲存連接字串的選項。
9. 在 **「設定選擇語句」** 步驟中,選擇「影片」資料庫表並選擇所有列。
10. 在 **「測試查詢**」步驟中,按下「完成」按鈕。
11. 回到 **「選擇資料來源**」步驟中,選擇要顯示的欄位的標題列和資料欄位的「Id」欄(參見圖)。
12. 按下「確定」按鈕關閉精靈。

[![選擇資料來源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**圖 05**: 選擇資料來源([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image10.png))

[![選擇資料文字與值欄位](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**圖 06**:選擇資料文字與值欄位([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image12.png))

完成上述步驟后,組合Box將綁定到SqlDataSource控制項,該控制項表示「電影」資料庫表中的影片。 頁面的源類似於清單 2(我稍微清理了格式)。

**清單 2 - 電影.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

請注意,ComboBox 控制件具有指向 SqlDataSource 控制件的 DataSourceID 屬性。 在瀏覽器中打開頁面時,將顯示資料庫中的影片清單(參見圖 7)。 您可以透過在組合盒中鍵入影片從清單中選取影片或輸入新影片。

[![顯示電影清單](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**圖 07**: 顯示電影列表([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>設定下拉式式

您可以使用組合盒下拉列表樣式屬性更改組合框的行為。 此屬性接受可能存在的值:

- 下拉 - (預設值) 當您按下箭頭並且可以輸入自訂值時,組合框將顯示下拉清單。
- 簡單 - 組合框會自動顯示下拉清單,您可以輸入自訂值。
- 下拉清單 - 組合框的工作方式與下拉清單控制項類似。

下拉清單和「簡單」之間的不同是顯示項目清單時。 在 Simple 的情況下,當您將焦點移動到組合框時,將立即顯示清單。 在下拉清單的情況下,必須按一下箭頭才能看到專案清單。

"下拉清單"值使組合盒控制項的工作方式與標準的下拉清單控制項類似。 然而,這裡有一個重要的區別。 較舊版本的 Internet Explorer 顯示具有無限 z 索引的下拉清單控制項,因此該控制項將顯示在放置在其前面的任何控制項的前面。 由於組合&lt;框呈現 HTML&gt;div&lt;標籤&gt;而不是 HTML 選擇 標記,因此組合框正確尊重 z 排序。

## <a name="setting-the-autocompletemode"></a>設定自動完成模式

您可以使用 ComboBox 自動完成模式屬性來指定當有人在組合框中鍵入文本時會發生什麼情況。 此屬性接受以下可能的值:

- 無 - (默認值) 組合框不提供任何自動完成行為。
- 建議 - 組合框顯示清單,並突出顯示清單中的匹配項(參見圖 8)。
- 附加 - 組合框不顯示清單,它將匹配項從清單中追加到已鍵入的內容(參見圖 9)。
- 建議應用 - 組合框都會顯示清單並將匹配項從清單中追加到已鍵入的內容上(參見圖 10)。

[![組合盒提出建議](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**圖 08**: 組合框提出建議([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image16.png))

[![組合盒附加符合文字](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**圖 09**: 組合盒中的文字([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image18.png))

[![組合框建議與新增](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**圖10**: 組合框建議與新增([按下以檢視全尺寸影像](how-do-i-use-the-combobox-control-cs/_static/image20.png))

## <a name="summary"></a>總結

在本教學中,您學習了如何使用 ComboBox 控件來顯示一組固定的專案。 我們將組合框控件綁定到靜態項集和資料庫表。 最後,您學習了如何通過設置其下拉風格和自動完成模式屬性來修改組合盒的行為。

> [!div class="step-by-step"]
> [下一步](how-do-i-use-the-combobox-control-vb.md)
