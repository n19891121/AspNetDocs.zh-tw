---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 顯示資料庫資料表 (VB) :微軟文件
author: rick-anderson
description: 在本教程中,我將演示顯示一組資料庫記錄的兩種方法。 我在 HTML ta...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b03e6a0d2bf7d2bf59ba4dca3076fa306d3fed4
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541893"
---
# <a name="displaying-a-table-of-database-data-vb"></a>顯示資料庫資料的資料表 (VB)

由[微軟](https://github.com/microsoft)

[下載 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> 在本教程中,我將演示顯示一組資料庫記錄的兩種方法。 我在 HTML 表中顯示了兩種格式化一組資料庫記錄的方法。 首先,我將演示如何直接在視圖中設置資料庫記錄的格式。 接下來,我將演示如何在格式化資料庫記錄時利用部分。

本教學的目的是解釋如何在 mVC 應用程式中顯示 ASP.NET 資料庫數據的 HTML 表。 首先,您將瞭解如何使用 Visual Studio 中包含的基架工具生成自動顯示一組記錄的檢視。 接下來,您將學習如何在格式化資料庫記錄時使用部分範本。

## <a name="create-the-model-classes"></a>建立模型類

我們將從「電影」資料庫表中顯示記錄集。 「影片」資料庫表包含以下欄:

<a id="0.4_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| Id | Int | False |
| Title | 恩瓦爾查爾 (200) | False |
| 導演 | 恩瓦爾查爾 (50) | False |
| 發佈日期 | Datetime | False |

為了在ASP.NET MVC 應用程式中表示"電影"表,我們需要創建一個模型類。 在本教學中,我們使用Microsoft實體框架創建模型類。

> [!NOTE] 
> 
> 在本教學中,我們使用Microsoft實體框架。 但是,請務必瞭解,您可以使用各種不同的技術與資料庫進行交互,從ASP.NET MVC 應用程式(包括 LINQ 到 SQL、NHibernate 或ADO.NET)。

依以下步驟啟動實體資料模型精靈:

1. 右鍵按一下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇選單選項 **「添加、新建專案**」。
2. 選擇 **「資料**」類別並選擇**ADO.NET 實體資料模型**樣本。
3. 為資料模型指定名稱 *「MoviesDBModel.edmx」,* 然後單擊 **「添加**」按鈕。

按下「添加」按鈕後,將顯示實體數據模型嚮導(參見圖 1)。 按照以下步驟完成精靈:

1. 在 **「選擇模型內容」** 步驟中,選擇「**從資料庫產生**」選項。
2. 在 **「選擇數據連接**」步驟中,使用*MoviesDB.mdf*數據連接和名稱 *「電影 DB 實體*」來設置連接設置。 按 **[下一步]** 按鈕。
3. 在 **「選擇資料庫物件**」步驟中,展開「表」節點,選擇「影片」表。 輸入命名空間*模型*,然後按下 **「完成」** 按鈕。

[![將 LINQ 建立 SQL 類別](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**圖 01**: 建立 LINQ 到 SQL 類別 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image2.png))

完成實體數據模型嚮導後,將打開實體數據模型設計器。 設計器應顯示影片實體(參見圖 2)。

[![實體資料模型設計器](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**圖 02**: 實體資料模型設計器 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image4.png))

在繼續之前,我們需要作出一個改變。 實體數據嚮導生成一個名為 *「電影」* 的模型類,該類表示"影片"資料庫表。 由於我們將使用「電影」類來表示特定影片,因此我們需要將類的名稱修改為 *「電影*」而不是 *「電影*」(單數而不是複數)。

按兩下設計器表面上的類的名稱,並將類的名稱從「影片」更改為「影片」。。 進行此更改後,按下 **「保存**」按鈕(軟盤的圖示)以生成 Movie 類。

## <a name="create-the-movies-controller"></a>建立影片控制器

現在,我們有一種方法來表示我們的資料庫記錄,我們可以創建一個控制器,返回電影的集合。 在可視化工作室解決方案資源管理器視窗中,右鍵單擊"控制器"資料夾並選擇功能表選項 **'添加控制器**"(參見圖 3)。

[![新增控制器選單](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**圖 03**: 新增控制器選單 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image6.png))

出現 **「添加控制器」** 對話方塊時,輸入控制器名稱「電影控制器」(參見圖 4)。 按下「**新增**」按鈕以新增新控制器。

[![新增控制器對話框](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**圖 04**: 新增控制器對話框([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image8.png))

我們需要修改由 Movie 控制器公開的 Index() 操作,以便它返回資料庫記錄集。 修改控制器,使其看起來像清單 1 中的控制器。

**清單1 = 控制器\電影控制器.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

在清單 1 中,電影 DB 實體類用於表示 MoviesDB 資料庫。 表達式*實體。MovieSet.ToList()* 從「影片」資料庫表中返回所有影片集。

## <a name="create-the-view"></a>建立檢視

在 HTML 表中顯示一組資料庫記錄的最簡單方法是利用 Visual Studio 提供的基架。

通過選擇功能表選項 **「生成」、「生成解決方案**」來構建應用程式。 在打開 **「添加檢視**」對話方塊之前,必須生成應用程式,否則數據類不會顯示在對話框中。

右鍵按一下索引() 操作並選擇功能表選項 **「添加檢視**」(參見圖 5)。

[![新增檢視](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**圖 05**: 新增檢視 ([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image10.png))

在 **'新增檢視'** 對話框中, 選擇標籤為「**建立強類型檢視」 選單的欄位**。 選擇「影片」類別作為**檢視資料類別**。 選擇 *「清單*」作為**檢視內容**(參見圖 6)。 選擇這些選項將生成顯示影片清單的強類型視圖。

[!['新增檢視"對話框](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**圖 06**: 新增檢視對話框([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image12.png))

按下「**添加**」按鈕後,將自動生成清單 2 中的檢視。 此檢視包含遍遍遍電影集合並顯示影片的每個屬性所需的代碼。

**清單 2 = 檢視\影片_索引.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

您可以通過選擇功能表選項 **「除錯」、「開始除錯**」(或點擊 F5 鍵)來執行應用程式。 運行應用程式將啟動 Internet 資源管理員。 如果您導航到 /Movie URL,您將看到圖 7 中的頁面。

[![電影表](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**圖 07**: 電影表([按下以檢視全尺寸影像](displaying-a-table-of-database-data-vb/_static/image14.png))

如果您不喜歡圖 7 中資料庫記錄網格的外觀,則只需修改 Index 視圖即可。 例如,您可以通過修改索引檢視將*日期釋放*標頭更改為*發佈日期釋放*日期。

## <a name="create-a-template-with-a-partial"></a>建立產生部分的樣本

當視圖變得過於複雜時,最好開始將視圖分解為部分視圖。 使用部分使您的檢視更易於理解和維護。 我們將創建一個部分,我們可以用作範本來格式化每個影片資料庫記錄。

依以下步驟建立部分:

1. 右鍵按兩下「檢視」+影片資料夾,然後選擇功能表選項 **「添加檢視**」。
2. 選中標記為「*創建部分檢視 (.ascx)」的*複選框。
3. 命名部分*影片樣本*。
4. 選中標記為「**創建強類型檢視」的**複選框。
5. 選擇「影片」 作為*檢視資料類別*。
6. 選擇「空」作為*檢視內容*。
7. 按下「**新增**」按鈕將部分新增到專案中。

完成這些步驟后,將「電影範本」部分修改為類似於清單 3。

**清單3 = 檢視\電影_電影範本.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

清單3中的部分包含一行記錄的範本。

清單4中修改後的索引視圖使用影片範本部分。

**清單4 = 檢視\影片_索引.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

清單 4 中的檢視包含一個「每個」迴圈,該迴圈遍歷了所有影片。 對於每個影片,影片範本部分用於格式化影片。 通過調用 Render 部分() 説明器方法來呈現影片範本。

修改後的 Index 檢視呈現的資料庫記錄的 HTML 表與同一個表。 但是,視圖已大大簡化。

Render部分() 方法不同於大多數其他幫助器方法,因為它不返回字串。 因此,必須&lt;使用 %html.render 部分() %&gt;而不是&lt;%= html.render 部分() %&gt;呼叫 render 部分() 方法。

## <a name="summary"></a>總結

本教學的目的是解釋如何在 HTML 表中顯示一組資料庫記錄。 首先,您學習了如何通過利用 Microsoft 實體框架從控制器操作返回一組資料庫記錄。 接下來,您學習了如何使用 Visual Studio 基架生成自動顯示專案集合的視圖。 最後,您學習了如何通過利用部分視圖來簡化視圖。 您學習了如何使用部分作為範本,以便可以格式化每個資料庫記錄。

> [!div class="step-by-step"]
> [前一個](creating-model-classes-with-linq-to-sql-vb.md)
> [下一個](performing-simple-validation-vb.md)
