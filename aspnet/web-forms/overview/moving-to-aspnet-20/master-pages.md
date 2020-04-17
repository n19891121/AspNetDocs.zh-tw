---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版頁 |微軟文件
author: rick-anderson
description: 成功網站的關鍵元件之一是外觀一致。 在ASP.NET 1.x 中,開發人員使用使用者控制件來複製通用頁面 elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543180"
---
# <a name="master-pages"></a>主版頁面

由[微軟](https://github.com/microsoft)

> 成功網站的關鍵元件之一是外觀一致。 在ASP.NET 1.x 中,開發人員使用使用者控制件跨Web應用程式複製公共頁面元素。 雖然這當然是一個可行的解決方案,但使用使用者控件確實有一些缺點。 例如,更改使用者控制項的位置需要更改到網站中的多個頁面。 在頁面上插入后,使用者控件也不會在"設計"視圖中呈現。

成功網站的關鍵元件之一是外觀一致。 在ASP.NET 1.x 中,開發人員使用使用者控制件跨Web應用程式複製公共頁面元素。 雖然這當然是一個可行的解決方案,但使用使用者控件確實有一些缺點。 例如,更改使用者控制項的位置需要更改到網站中的多個頁面。 在頁面上插入后,使用者控件也不會在"設計"視圖中呈現。

ASP.NET 2.0 引入母版頁作為保持一致外觀和感覺的一種方式,正如您很快就會看到的那樣,母版頁代表了對使用者控制方法的重大改進。

## <a name="why-master-pages"></a>為什麼選擇母版頁?

您可能想知道為什麼 ASP.NET 2.0 需要母版頁。 畢竟,網站開發人員已經在ASP.NET 1.x 中使用使用者控制式件在頁面之間共用內容區域。 實際上,使用者控件是創建公共佈局的不太理想的解決方案的原因有很多。

使用者控件實際上不定義頁面佈局。 相反,它們定義頁面的一部分的佈局和功能。 這兩者之間的區別很重要,因為它使用戶控制解決方案的可管理性變得更加困難。 例如,如果要更改頁面上的使用者控制項的位置,必須編輯顯示使用者控制件的實際頁面。 如果你只有幾頁,這很好,但在大型網站,它迅速成為一個網站管理噩夢!

使用使用者控制定義公共佈局的另一個缺點是ASP.NET本身的體系結構。 如果更改了使用者控件的任何公共成員,則需要重新編譯使用使用者控制件的所有頁面。 反過來,ASP.NET將在首次訪問頁面時重新 JIT。 這再次產生了一個不可擴展的體系結構和大型網站的網站管理問題。

ASP.NET 2.0 中的母版頁很好地解決了這兩個問題(以及更多問題)。

## <a name="how-master-pages-work"></a>母版頁的工作原理

母版頁類似於其他頁面的範本。 應在其他頁面(即功能表、邊框等)之間共用的頁面元素將添加到母版頁中。 將新頁面添加到網站時,可以將它們與母版頁相關聯。 與母版頁關聯的頁面稱為**內容頁**。 默認情況下,內容頁從母版頁中呈現外觀。 但是,在創建母版頁時,可以定義內容頁可以替換為其自己的內容的部分內容。 這些部分使用ASP.NET 2.0 中引入的新控制件進行定義;**ContentPlaceHolder 控制項**。

母版頁可以包含任意數量的 Content PlaceHolder 控件(或根本沒有。在內容頁上,"ContentPlace Holder"控件中的內容將顯示在**內容**控件中,這是 ASP.NET 2.0 中的另一個新控制項。 預設情況下,內容頁 內容控制項為空,以便您可以提供自己的內容。 如果要使用內容控制件內母版頁中的內容,可以執行此操作,正如您將在此模組的後面部分看到的。 內容控件通過內容控制件的「內容霍爾德ID」屬性映射到 ContentPlaceHolderId 控制件。 下面的代碼將內容控件映射到主頁上稱為 mainBody 的 Content Place Holder 控件。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 您經常會聽到人們將母版頁描述為其他頁面的基類。 這實際上不是真的。 母版頁和內容頁之間的關係不是繼承關係。

**圖 1**顯示了母版頁和關聯的內容頁,因為它們出現在 Visual Studio 2005 中。 您可以在母版頁中查看 ContentPlaceHolder 控件,並在內容頁中看到相應的內容控制件。 請注意,內容霍爾德持有人外部的母版頁內容可見,但在內容頁中顯示為灰色。 只有 ContentPlaceHolder 中的內容可以由內容頁取代。 來自母版頁的所有其他內容是不可改變的。

![母版頁及其關聯內容頁](master-pages/_static/image1.jpg)

**圖 1**: 母版頁及其關聯內容頁

## <a name="creating-a-master-page"></a>建立母版頁

要創建新的母版頁,

1. 打開 Visual Studio 2005 並創建新網站。
2. 按下"檔,新建,檔"。
3. 從"添加新項目"對話框中選擇主檔,如圖**2**所示。
4. 按一下 [加入]。

![建立新母版頁](master-pages/_static/image2.jpg)

**圖 2**: 建立新母版頁

請注意,母版頁的檔案副檔名是 *.master*。 這是母版頁與普通頁面不同的方式之一。 另一個主要區別是,母版頁代替指令@Page,包含一@Master個 指令。 切換到您剛剛建立的母版頁的源檢視並查看代碼。

默認情況下,新的母版頁將有一個 ContentPlaceHolder 控件。 在大多數情況下,首先創建公共頁面元素,然後插入需要自定義內容的 ContentPlace Holder 控件更有意義。 在這些情況下,開發人員將希望刪除預設的 ContentPlaceHolder 控件,並在頁面開發時插入新的控制項。 ContentPlaceHolder 控件雖然確實顯示大小調整句柄,但它們不會調整大小。 ContentPlaceHolder 控件的大小會自動基於它包含的內容,但有一個例外;如果將 ContentPlaceHolder 控制元件放置在塊元素(如表單元格)內,則該控制項將根據元素的大小進行大小調整。

## <a name="lab-1-working-with-master-pages"></a>實驗室 1 使用母版頁

在本實驗中,您將創建一個新的母版頁,並定義三個 ContentPlaceHolder 控制件。 然後,您將創建新的內容頁,並至少從其中一個 ContentPlace Holder 控制中替換內容。

1. 創建母版頁並插入內容霍爾德控制項。 

    1. 如上文所述,創建新的母版頁。
    2. 移除預設的「內容放置」 控制器。
    3. 通過按一下控制的上邊框,然後點擊鍵盤上的 DEL 鍵將其刪除,選擇 ContentPlaceHolder 控制件。
    4. 使用*標題和側*範本插入新錶,如圖 3 所示。 將寬度和高度更改為 90%,以便整個表在設計器中可見。

![](master-pages/_static/image3.jpg)

**圖 3**

1. 將游標放入表的每個儲存格中,並將*valign*屬性設定為*頂端*。
2. 在工具箱中,在表的頂部單元格(標題單元格)中插入 ContentPlaceHolder 控制件。
3. 插入此 ContentPlaceHolder 控件時,您會注意到行高度將佔用幾乎整個頁面,如圖 4 所示。 在這一點上不要擔心。

![空白空間與內容霍爾德位於同一單元格中](master-pages/_static/image1.gif)

**圖 4**: 空白空間與內容霍爾德位於同一儲存格中

1. 將 Content PlaceHolder 控件放在其他兩個單元格中。 插入其他 ContentPlaceHolder 控制程式後,表單元格的大小應如您所料。 該頁現在應類似於**圖 5**所示的頁面。

![包含所有內容位置擁有者控制件的主控形狀。 請注意,頭單元格的單元格高度現在正是它應該的](master-pages/_static/image2.gif)

**圖 5**: 包含所有內容霍爾德控制項的主控形狀。 請注意,頭單元格的單元格高度現在正是它應該的

1. 在三個 ContentPlaceHolder 控制件中的每個控制項中輸入您選擇的文字。
2. 將母版頁另存為練習1.master。
3. 創建新的 Web 窗體並將其與練習 1.master 頁相關聯。
4. 選擇檔,新建,檔在可視化工作室2005年。
5. 在「添加新項目」對話框中選擇 **「Web 窗體**」 。。
6. 確保選中"選擇母版頁"複選框,如圖 6 所示。

![新增的內容頁](master-pages/_static/image3.gif)

**圖 6**: 新增新的內容頁

1. 按一下 [加入]。
2. 在「選擇母版頁對話框中選擇練習1.master,如圖 7 所示。
3. 按一下「確定」以添加新內容頁。

新內容頁顯示在 Visual Studio 中,母版頁上每個 Content PlaceHolder 控制件都有一個內容控制件。 預設情況下,內容控制項為空,以便您可以添加自己的內容。 如果您希望他們使用母版頁上的 ContentPlaceHolder 控件中的內容,只需單擊智慧標記符號(控件右上角的小黑箭頭),然後從智慧標記中選擇 *「默認到母版內容*」,如圖**8**所示。 執行此操作時,功能表項將更改為 *「創建自訂內容*」 。 此時按這裏選它會從母版頁中刪除內容,允許您為該特定內容控制項定義自訂內容。

![將內容控制檔設定為預設為母版頁內容](master-pages/_static/image4.gif)

**圖 7**: 將內容控制檔設定為預設為母版頁內容

## <a name="connecting-master-page-and-content-pages"></a>連接母版頁與內容頁

母版頁和內容頁之間的關聯可以通過以下四種不同方式之一進行配置:

- 指令的@Page<strong>母版頁面檔案</strong>屬性
- 在代碼中設置**Page.MasterPageFile**屬性。
- 應用程式設定檔中的**&lt;頁面&gt;** 元素(應用程式根資料夾中的 Web.config)
- 子資料夾設定檔中的**&lt;頁面&gt;** 元素(子資料夾中的 Web.config)

## <a name="masterpagefile-attribute"></a>母版檔案屬性

MasterPageFile 屬性使將母版頁應用於特定ASP.NET頁面變得容易。 當您選中 **「選擇母版頁**」複選框時,它也是用於應用母版頁的方法,就像練習 1 中所做的那樣。

## <a name="setting-pagemasterpagefile-in-code"></a>設定頁面.MasterPage檔案代碼

通過在代碼中設置 MasterPageFile 屬性,可以在運行時將特定的母版頁應用於您的內容。 在可能需要根據使用者角色或其他一些條件應用特定母版頁的情況下,這非常有用。 必須在 PreInit 方法中設置 MasterPageFile 屬性。 如果在 PreInit 方法之後設置,將引發無效操作異常。 正在設置此屬性的頁面還必須具有「內容」控件作為該頁的頂級控制項。 否則,在設置 MasterPageFile 屬性時,將引發 HTTPException。

## <a name="using-the-ltpagesgt-element"></a>使用&lt;頁面&gt;元素

您可以通過在 Web.config&lt;&gt;檔的頁面 元素中設定 masterPageFile 屬性來設定頁面的母版頁。 使用此方法時,請記住,應用程式結構中較低的 Web.config 檔可以覆蓋此設置。 @Page指令中的任何 MasterPageFile 屬性集也將覆蓋此設定。 使用&lt;頁面&gt;元素可以創建可在特定資料夾或檔中在必要時重寫*的主版*頁變得簡單。

## <a name="properties-in-master-pages"></a>母版頁中的屬性

母版頁只需在母版頁中公開這些屬性,即可公開屬性。 例如,以下代碼定義名為「某些屬性」的屬性:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

要從「內容」頁存取「某些屬性」屬性,您需要使用「主」屬性,如下所示:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>巢狀母版頁

母版頁是確保大型 Web 應用程式的共同外觀的完美解決方案。 但是,大型網站的某些部分共用公共介面,而其他部分共用不同的介面的情況並不少見。 為了滿足這一需求,多個母版頁是完美的解決方案。 但是,這仍然不能解決大型應用程式可能具有某些元件(例如功能表)這一事實,這些元件僅在網站的某些部分之間共用的所有頁面和其他元件之間共用。 對於這種情況,嵌套母版頁很好地滿足了需求。 正如您所看到的,普通母版頁由母版頁和內容頁組成。 在嵌套母版頁的情況下,有兩個母版頁;父主控形狀和子母版。 子母版頁也是內容頁,其母版頁是父母版頁。

下面是典型母版頁的代碼:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

在嵌套主方案中,這將是父主控形狀。 另一個母版頁將使用此頁作為其母版頁,該代碼如下所示:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

請注意,在這種情況下,子母版也是父主控形狀的內容頁。 所有子主控內容都顯示在內容控件中,該控件從父級的 ContentPlaceHolder 控件中獲取其內容。

> [!NOTE]
> 設計器支援不適用於嵌套母版頁。 使用嵌套母版進行開發時,需要使用源視圖。

此視頻顯示了使用嵌套母版頁的演練。

![](master-pages/_static/image1.png)

[開啟全螢幕視訊](master-pages/_static/nested1.wmv)

![選擇母版頁](master-pages/_static/image4.jpg)

**圖 8**: 選擇母版頁
