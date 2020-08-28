---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
title: '如何? 使用 ComboBox 控制項？  (C # ) |Microsoft Docs'
author: rick-anderson
description: ComboBox 是 ASP.NET 的 AJAX 控制項，結合 TextBox 的彈性與使用者可以選擇的選項清單。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0bbf4134-04df-4226-8930-d5bb99e27128
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 035bcb2fb6cce246b904c295aba15efd17c2c232
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045061"
---
# <a name="how-do-i-use-the-combobox-control-c"></a>如何? 使用 ComboBox 控制項？ (C#)

由 [Microsoft](https://github.com/microsoft)

> ComboBox 是 ASP.NET 的 AJAX 控制項，結合 TextBox 的彈性與使用者可以選擇的選項清單。

本教學課程的目的是要說明 AJAX 控制項工具組 ComboBox 控制項。 ComboBox 的運作方式就像是標準 ASP.NET DropDownList 控制項和 TextBox 控制項之間的組合。 您可以從預先存在的專案清單中選取，或輸入新的專案。

下拉式方塊類似于「自動完成控制項」擴充項，但控制項用於不同的案例。 自動完成擴充項會查詢 web 服務來取得相符的專案。 相反地，ComboBox 控制項會以一組專案初始化。 當您使用大型 (資料集來處理大量資料時，使用 [自動完成擴充項] 是很合理的) 當您在處理一小部分的資料 (數十個汽車零件) 時，使用 ComboBox 控制項就很有意義。

## <a name="selecting-from-a-static-list-of-items"></a>從靜態專案清單中選取

讓我們從使用 ComboBox 控制項的簡單範例開始。 假設您想要在下拉式清單中顯示靜態的專案清單。 不過，您想要保持開啟清單未完成的可能性。 您想要允許使用者在清單中輸入自訂值。

我們會建立新的 ASP.NET Web Forms 頁面，並在頁面中使用 ComboBox 控制項。 將新的 ASP.NET 網頁新增至您的專案，並切換至設計檢視。

如果您想要在頁面中使用 ComboBox 控制項，則必須將 ScriptManager 控制項加入頁面中。 將 ScriptManager 控制項從 [AJAX 擴充功能] 索引標籤底下拖曳至設計工具介面上。 您應在頁面頂端新增 ScriptManager 控制項;您可以緊接在開頭的伺服器端 &lt; 表單標記下方加入它 &gt; 。

接下來，將 ComboBox 控制項拖曳至頁面上。 您可以使用其他 AJAX 控制項工具組控制項和控制項擴充項，在 [工具箱] 中找到 ComboBox 控制項 (查看圖 1) 。

[![建立名片的簡單表單](how-do-i-use-the-combobox-control-cs/_static/image1.jpg)](how-do-i-use-the-combobox-control-cs/_static/image1.png)

**圖 01**：從 [工具箱] 選取 ComboBox 控制項 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image2.png)) 

我們將使用 ComboBox 控制項來顯示靜態的選項清單。 使用者可以從下列三個選項的清單中選取特定的 spiciness 層級： [輕度]、[中] 和 [經常性 (]，請參閱 [圖 2]) 。

[![從靜態專案清單中選取](how-do-i-use-the-combobox-control-cs/_static/image2.jpg)](how-do-i-use-the-combobox-control-cs/_static/image3.png)

**圖 02**：從靜態專案清單中選取 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image4.png)) 

有兩種方式可以將這些選項新增至 ComboBox 控制項。 首先，當您將滑鼠停留在設計檢視中的控制項上方並開啟專案編輯器時，請選取 [編輯選項] 工作選項 (請參閱 [圖 3]) 。

[![編輯 ComboBox 專案](how-do-i-use-the-combobox-control-cs/_static/image3.jpg)](how-do-i-use-the-combobox-control-cs/_static/image5.png)

**圖 03**：編輯 ComboBox 專案 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image6.png)) 

第二個選項是在來源視圖的開頭和結尾 &lt; asp： ComboBox 標記之間加入專案清單 &gt; 。 [清單 1] 中的頁面包含已更新專案清單的 [已更新] ComboBox。

**清單 1-靜態 .aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample1.aspx)]

當您開啟 [清單 1] 中的頁面時，可以從下拉式方塊中選取其中一個預先存在的選項。 換句話說，ComboBox 的運作方式就像是 DropDownList 控制項一樣。

不過，您也可以選擇輸入新的選擇 (例如，不在現有清單中的 Super Spicy) 。 因此，ComboBox 也可以像 TextBox 控制項一樣運作。

無論您是否選擇預先存在的專案，或輸入自訂專案，當您提交表單時，您的選擇都會出現在標籤控制項中。 當您提交表單時，btnSubmit \_ Click 處理常式會執行並更新標籤 (請參閱 [圖 4]) 。

[![顯示選取的專案](how-do-i-use-the-combobox-control-cs/_static/image4.jpg)](how-do-i-use-the-combobox-control-cs/_static/image7.png)

**圖 04**：顯示選取的專案 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image8.png)) 

ComboBox 支援與 DropDownList 控制項相同的屬性，以便在提交表單之後，用來抓取選取的專案：

- SelectedItem：顯示所選取專案的 Text 屬性值。
- SelectedItem：顯示所選取專案的 Value 屬性值，或顯示在下拉式方塊中輸入的文字。
- SelectedValue 與 SelectedItem 相同，不同之處在于此屬性可讓您指定預設 (初始) 選取的專案。

如果您在下拉式方塊中輸入自訂選擇，則會將自訂選項同時指派給 SelectedItem 和 SelectedItem 屬性。

## <a name="selecting-the-list-of-items-from-the-database"></a>從資料庫中選取專案清單

您可以從資料庫中取出下拉式方塊所顯示的專案清單。 例如，您可以將 ComboBox 系結至 SqlDataSource 控制項、ObjectDataSource 控制項、LinqDataSource 或 EntityDataSource。

假設您想要在下拉式方塊中顯示電影清單。 您想要從電影資料庫資料表中取出電影清單。 請遵循下列步驟：

1. 建立名為 default.aspx 的頁面
2. 將 ScriptManager 控制項從 [工具箱] 中的 [AJAX 擴充功能] 索引標籤拖曳到頁面上，以將 ScriptManager 控制項加入頁面中。
3. 將 combobox 拖曳至頁面上，以將 ComboBox 控制項加入頁面中。
4. 在設計檢視中，將滑鼠停留在 ComboBox 控制項上方，然後選取 [ **選擇資料來源** ] 工作選項 (請參閱 [圖 5]) 。 [資料來源設定] 設定為 [已啟動]。
5. 在 [ **選擇資料來源** ] 步驟中，選取 [ &lt; 新增資料來源] &gt; 選項。
6. 在 [ **選擇資料來源類型** ] 步驟中，選取 [資料庫]。
7. 在 [ **選擇您的資料連線** ] 步驟中，選取您的資料庫 (例如，MoviesDB .mdf) 。
8. 在 [ **將連接字串儲存到應用程式佈建檔** ] 步驟中，選取儲存連接字串的選項。
9. 在 [ **設定 Select 語句** ] 步驟中，選取 [電影資料庫] 資料表，然後選取所有資料行。
10. 在 [ **測試查詢** ] 步驟中，按一下 [完成] 按鈕。
11. 回到 [ **選擇資料來源** ] 步驟中，選取要顯示之欄位的 [標題] 資料行，並選取 [資料] 欄位的 [識別碼] 資料行 (查看 [圖) ]。
12. 按一下 [確定] 按鈕以關閉嚮導。

[![選擇資料來源](how-do-i-use-the-combobox-control-cs/_static/image5.jpg)](how-do-i-use-the-combobox-control-cs/_static/image9.png)

**圖 05**：選擇資料來源 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image10.png)) 

[![選擇資料文字和值欄位](how-do-i-use-the-combobox-control-cs/_static/image6.jpg)](how-do-i-use-the-combobox-control-cs/_static/image11.png)

**圖 06**：選擇資料文字和值欄位 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image12.png)) 

完成上述步驟後，ComboBox 會系結至代表電影資料庫資料表中電影的 SqlDataSource 控制項。 頁面的來源看起來像 [清單 2] (我將格式化稍微) 。

**清單 2-default.aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-cs/samples/sample2.aspx)]

請注意，ComboBox 控制項有指向 SqlDataSource 控制項的 DataSourceID 屬性。 當您在瀏覽器中開啟頁面時，會顯示資料庫中的電影清單 (請參閱 [圖 7]) 。 您可以從清單中挑選電影，或在下拉式方塊中輸入電影來輸入新的電影。

[![顯示電影清單](how-do-i-use-the-combobox-control-cs/_static/image7.jpg)](how-do-i-use-the-combobox-control-cs/_static/image13.png)

**圖 07**：顯示電影清單 ([按一下以觀看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image14.png)) 

## <a name="setting-the-dropdownstyle"></a>設定 DropDownStyle

您可以使用 ComboBox DropDownStyle 屬性來變更 ComboBox 的行為。 這個屬性會接受可能的值：

- 下拉式 (預設值) 當您按一下箭號時，下拉式清單會顯示下拉式清單，而您可以輸入自訂值。
- 簡單-下拉式方塊會自動顯示下拉式清單，而您可以輸入自訂值。
- DropDownList-下拉式方塊的運作方式就像 DropDownList 控制項一樣。

下拉式清單和簡單的不同之處是顯示專案清單。 在簡單的情況下，當您將焦點移至下拉式方塊時，清單會立即顯示。 在下拉式清單中，您必須按一下箭號以查看專案清單。

DropDownList 值會使 ComboBox 控制項如同標準 DropDownList 控制項一樣運作。 不過，這裡有一個重要的差異。 舊版 Internet Explorer 會顯示具有無限 z 索引的 DropDownList 控制項，讓控制項出現在其前方的任何控制項前面。 因為 ComboBox 會轉譯 HTML &lt; div &gt; 標記而非 html 選取標記，所以下拉式方塊會 &lt; &gt; 正確地遵循 z 順序。

## <a name="setting-the-autocompletemode"></a>設定 Autocompletemode.none

您可以使用 ComboBox Autocompletemode.none 屬性來指定當有人將文字輸入 ComboBox 時，會發生什麼事。 這個屬性會接受下列可能的值：

- None- (預設值) ComboBox 不提供任何自動完成行為。
- 建議-下拉式方塊會顯示清單，並反白顯示清單中的相符專案 (請參閱 [圖 8]) 。
- 附加-下拉式方塊不會顯示清單，而會將相符的專案從清單附加到您輸入的內容 (請參閱 [圖 9]) 。
- SuggestAppend-下拉式方塊會顯示清單，並將清單中的相符專案附加到您輸入的內容 (請參閱 [圖 10]) 。

[![ComboBox 會提出建議](how-do-i-use-the-combobox-control-cs/_static/image8.jpg)](how-do-i-use-the-combobox-control-cs/_static/image15.png)

**圖 08**：下拉式方塊提出建議 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image16.png)) 

[![ComboBox 附加符合的文字](how-do-i-use-the-combobox-control-cs/_static/image9.jpg)](how-do-i-use-the-combobox-control-cs/_static/image17.png)

**圖 09**： ComboBox 附加相符的文字 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image18.png)) 

[![ComboBox 建議和附加](how-do-i-use-the-combobox-control-cs/_static/image10.jpg)](how-do-i-use-the-combobox-control-cs/_static/image19.png)

**圖 10**： ComboBox 建議和附加 ([按一下以查看完整大小的影像](how-do-i-use-the-combobox-control-cs/_static/image20.png)) 

## <a name="summary"></a>摘要

在本教學課程中，您已瞭解如何使用 ComboBox 控制項來顯示一組固定的專案。 我們將 ComboBox 控制項系結至一組靜態專案和資料庫資料表。 最後，您已瞭解如何藉由設定 DropDownStyle 和 Autocompletemode.none 屬性來修改 ComboBox 的行為。

> [!div class="step-by-step"]
> [下一個](how-do-i-use-the-combobox-control-vb.md)
