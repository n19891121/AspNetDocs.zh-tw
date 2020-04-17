---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 使用查看母版頁 (VB) 建立頁面佈局 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。 您可以使用...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 37b8d858c72357ebbe51458f76511a9672b01b4d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542491"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>使用檢視主版頁面建立頁面配置 (VB)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。 例如,可以使用檢視母版頁定義兩列頁面佈局,並為 Web 應用程式中的所有頁面使用兩列佈局。

## <a name="creating-page-layouts-with-view-master-pages"></a>使用檢視母版頁建立頁面配置

在本教學中,您將瞭解如何利用檢視母版頁為應用程式中的多個頁面創建通用頁面佈局。 例如,可以使用檢視母版頁定義兩列頁面佈局,並為 Web 應用程式中的所有頁面使用兩列佈局。

您還可以利用查看母版頁在應用程式中多個頁面之間共用常見內容。 例如,您可以將網站徽標、導航鏈接和橫幅廣告放在視圖母版頁中。 這樣,應用程式中的每個頁面都會自動顯示此內容。

在本教學中,您將瞭解如何創建新的檢視母版頁,並根據母版頁創建新的檢視內容頁。

### <a name="creating-a-view-master-page"></a>建立檢視母版頁

讓我們首先創建定義兩列佈局的檢視母版頁。 通過右鍵按下「檢視+共用」資料夾、選擇功能表選項 **「新增、新建專案**」以及選擇 MVC 檢視母版頁範本(參見圖 1),將新的檢視母版頁添加到 MVC 專案。

[![新增檢視母版頁](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**圖 01**: 新增檢視母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))

您可以在應用程式中創建多個檢視母版頁。 每個檢視母版頁可以定義不同的頁面佈局。 例如,您可能希望某些頁面具有兩列佈局和其他頁面具有三列佈局。

檢視母版頁看起來非常類似於標準ASP.NET MVC 檢視。 但是,與普通視圖不同,視圖母版頁包含一個或多個`<asp:ContentPlaceHolder>`標記。 這些`<contentplaceholder>`標記用於標記可在單個內容頁中重寫的母版頁區域。

例如,清單 1 中的檢視母版頁定義兩列佈局。 它包含兩`<contentplaceholder>`個標記。 每`<ContentPlaceHolder>`列一列。

**清單1 |`Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

清單1中的檢視母版頁的正文包含兩`<div>`個對應於兩列的標記。 "級聯樣式表"列類應用於這兩個`<div>`標記。 此類在母版頁頂部聲明的樣式表中定義。 您可以通過切換到"設計"視圖來預覽視圖母版頁的呈現方式。 按一下原始碼編輯器左下角的「設計」選項卡(參見圖 2)。

[![在設計器中預覽母版頁](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**圖 02**: 預覽設計器中的母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))

### <a name="creating-a-view-content-page"></a>建立檢視內容頁面

創建檢視母版頁後,可以基於檢視母版頁創建一個或多個視圖內容頁。 例如,您可以通過右鍵單擊「檢視+主頁」資料夾、選擇 **「新增、新建專案」、** 選擇**MVC 查看內容頁**樣本、輸入名稱 Index.aspx 以及單擊「新增」按鈕(參見圖 3)為主控制器建立索引視圖內容頁。

[![新增檢視內容頁](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**圖 03**: 新增檢視內容頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))

按下「添加」按鈕後,將出現一個新對話框,使您能夠選擇視圖母版頁以與檢視內容頁關聯(參見圖 4)。 您可以導航到我們在上一節中創建的 Site.master 檢視母版頁。

[![選擇母版頁](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**圖 04**: 選擇母版頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))

基於 Site.master 母版頁建立新的檢視內容頁後,您將在清單 2 中獲取該檔。

**清單2 |`Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

請注意,此檢視包含一個`<asp:Content>`對應於視圖母版頁中每個`<asp:ContentPlaceHolder>`標記的標記。 每個`<asp:Content>`標記都包含 ContentPlace HolderID`<asp:ContentPlaceHolder>`屬性, 該屬性指向它覆蓋的特定。

此外,請注意,清單 2 中的內容檢視頁不包含任何正常的打開和關閉 HTML 標記。 例如,它不包含打開和關閉`<html>`或`<head>`標記。 所有正常的打開和關閉標記都包含在檢視母版頁中。

要在檢視內容頁中顯示的任何內容都必須放置在`<asp:Content>`標記中。 如果將這些標記之外放置任何 HTML 或其他內容,則當您嘗試查看頁面時,將出現錯誤。

您無需覆蓋內容檢視頁中母`<asp:ContentPlaceHolder>`版頁中的每個標記。 僅當要將`<asp:ContentPlaceHolder>`標記替換為特定內容時,才需要覆蓋標記。

例如,清單 3 中修改的索引檢視僅包含`<asp:Content>`兩 個標記。 每個`<asp:Content>`標記都包含一些文本。

**清單3 |`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

當請求清單 3 中的檢視時,它將呈現圖 5 中的頁面。 請注意,視圖呈現具有兩列的頁面。 此外,請注意,檢視內容頁中的內容將與視圖母版頁中的內容合併。

[![索引檢視內容頁](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**圖 05**: 索引檢視內容頁 ([按下以檢視全尺寸影像](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>變更檢視母版頁內容

在使用檢視母版頁時,您幾乎立即遇到的一個問題是,當請求不同的檢視內容頁時,會修改視圖母版頁內容。 例如,您希望 Web 應用程式中的每個頁面都有唯一的標題。 但是,標題在視圖母版頁中聲明,而不是在視圖內容頁中聲明。 那麼,如何為每個檢視內容頁面自定義頁面標題?

有兩種方法可以修改檢視內容頁顯示的標題。 首先,您可以將頁面標題分配給檢視內容頁頂部聲明的`<%@ page %>`指令的標題屬性。 例如,如果要將頁面標題「超級大網站」分配給索引檢視,則可以在 Index 視圖的頂部包括以下指令:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

當「索引」檢視呈現給瀏覽器時,所需的標題將顯示在瀏覽器標題列中:

[![瀏覽器標題列](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

主視圖頁必須滿足一個重要要求,以便標題屬性正常工作。 視圖母版頁必須包含`<head runat="server">`標記,而不是其標題的`<head>`正常 標記。 如果`<head>`標記不包含 runat_"server"屬性,則標題將不會顯示。 默認檢視母版頁包括所需的`<head runat="server">`標記。

從單個檢視內容頁修改母版頁內容的另一種方法是包裝要在`<asp:ContentPlaceHolder>`標記中修改的區域。 例如,假設您不僅希望更改標題,還要更改由母版視圖頁呈現的元標記。 清單4中的主視圖頁在其`<asp:ContentPlaceHolder>``<head>`標記中包含一個標記。

**清單4 |`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

請注意,`<asp:ContentPlaceHolder>`清單 4 中的標記包括預設內容:默認標題和預設元標記。 如果不在單個檢視內容頁中`<asp:ContentPlaceHolder>`覆蓋此標記,則將顯示默認內容。

清單5中的內容檢視頁將覆蓋`<asp:ContentPlaceHolder>`標記,以便顯示自定義標題和自定義元標記。

**清單5 |`Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>總結

本教程為您提供查看母版頁和查看內容頁的基本介紹。 您學習了如何創建新的檢視母版頁,並基於它們創建檢視內容頁。 我們還研究了如何從特定視圖內容頁修改視圖母版頁的內容。

> [!div class="step-by-step"]
> [前一個](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [下一個](passing-data-to-view-master-pages-vb.md)
