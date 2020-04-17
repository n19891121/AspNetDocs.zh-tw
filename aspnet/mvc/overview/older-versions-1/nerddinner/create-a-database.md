---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 建立資料庫 | Microsoft 文件
author: rick-anderson
description: 步驟 2 顯示了創建資料庫的步驟,這些資料庫包含我們 NerdDinner 應用程式的所有晚餐和 RSVP 數據。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: d0b87e4a6a27b37d2dbaa6d5b871da477b25586d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541607"
---
# <a name="create-a-database"></a>建立資料庫

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第2步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。
> 
> 步驟 2 顯示了創建資料庫的步驟,這些資料庫包含我們 NerdDinner 應用程式的所有晚餐和 RSVP 數據。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-2-creating-the-database"></a>神經晚餐步驟 2:創建資料庫

我們將使用資料庫來儲存我們NerdDinner應用程式的所有晚餐和RSVP數據。

以下步驟顯示了使用免費 SQL Server Express 版本創建資料庫(您可以使用[Microsoft Web 平臺安裝程式](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 輕鬆安裝)。 我們將編寫的所有代碼都適用於 SQL Server Express 和完整 SQL Server。

### <a name="creating-a-new-sql-server-express-database"></a>建立新的 SQL Server Express 資料庫

我們將從右鍵單擊 Web 專案開始,然後選擇 **「新增新&gt;專案」** 選單命令:

![](create-a-database/_static/image1.png)

這將彈出可視化工作室的「添加新項目」對話框。 我們將按「資料」類別進行篩選,然後選擇「SQL 伺服器資料庫」項範本:

![](create-a-database/_static/image2.png)

我們將命名要創建的 SQL Server Express 資料庫「NerdDinner.mdf」,然後點擊確定。 然後,Visual Studio 會詢問我們是否要將此檔添加到\_我們的 @App 資料目錄(該目錄已設置包含讀取和寫入安全 ACL):

![](create-a-database/_static/image3.png)

我們將按下「是」,我們將創建新資料庫並將其添加到解決方案資源管理器中:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>在資料庫建立表格

我們現在有一個新的空資料庫。 讓我們向它添加一些表。

為此,我們將導航到 Visual Studio 中的「伺服器資源管理器」選項卡視窗,這使我們能夠管理資料庫和伺服器。 儲存在應用程式的\_@App 資料資料夾中的 SQL Server Express 資料庫將自動顯示在伺服器資源管理器中。 我們可以選擇使用「伺服器資源管理員」視窗頂部的「連接到資料庫」圖示,將其他 SQL Server 資料庫(本地資料庫和遠端資料庫)新增到清單中:

![](create-a-database/_static/image5.png)

我們將向NerdDinner資料庫添加兩個錶 - 一個用於存儲我們的晚餐,另一個用於跟蹤 RSVP 接受的接收。 我們可以通過右鍵按一下資料庫中的「表」資料夾並選擇「新增新表」選單命令來建立新錶:

![](create-a-database/_static/image6.png)

這將打開一個表設計器,允許我們配置表的架構。 對於我們的「Dinners」表,我們將添加 10 列數據:

![](create-a-database/_static/image7.png)

我們希望「DinnerID」列是表的唯一主鍵。 我們可以通過右鍵單擊「DinnerID」列並選擇「設定主鍵」功能表項來配置此項:

![](create-a-database/_static/image8.png)

除了使 DinnerID 成為主鍵外,我們還希望將其配置為「標識」列,該列的值隨著新數據行添加到表中而自動遞增(這意味著第一個插入的 Dinner 行的 DinnerID 為 1,第二個插入的行的 DinnerID 為 2,等等)。

為此,我們可以選擇"DinnerID"列,然後使用"列屬性"編輯器將列上的"(即標識)"屬性設置為"是"。 我們將使用標準標識預設值(從 1 開始,在每個新的 Dinner 行上增加 1):

![](create-a-database/_static/image9.png)

然後,我們將通過鍵入 Ctrl-S 或使用 **「&gt;檔儲存」** 選單命令來保存我們的表。 這將提示我們命名表。 我們將將其命名為「晚餐」:

![](create-a-database/_static/image10.png)

然後,我們新的 Dinners 表將顯示到伺服器資源管理器中的資料庫中。

然後,我們將重複上述步驟,並創建一個"RSVP"表。 此表包含 3 列。 我們將將 RsvpID 列設定為主鍵,並使其成為識別列:

![](create-a-database/_static/image11.png)

我們將保存它,並給它的名字"RSVP"。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>設定表之間的外鍵關係

現在,我們的資料庫中有兩個表。 我們最後一個架構設計步驟是在這兩個表之間建立「一對多」關係,以便我們可以將每個 Dinner 行與應用於它的零個或多個 RSVP 行相關聯。 為此,我們將配置 RSVP 表的「DinnerID」列,以便與「Dinners」表中的「DinnerID」列具有外鍵關係。

為此,我們將在伺服器資源管理器中按兩下表設計器中打開 RSVP 表。 然後,我們將選擇其中的"DinnerID"列,右鍵單擊,然後選擇"關係..."內容選單指令:

![](create-a-database/_static/image12.png)

這將彈出一個對話框,我們可以用它來設置表之間的關係:

![](create-a-database/_static/image13.png)

我們將按下「添加」按鈕以向對話框添加新關係。 添加關係後,我們將將屬性網格中的"表和列規範"樹視圖節點擴展到對話框的右側,然後單擊"..."按鈕右方:

![](create-a-database/_static/image14.png)

單擊"..."按鈕將彈出另一個對話框,允許我們指定關係中涉及哪些表和列,並允許我們命名關係。

我們將主鍵表更改為「Dinners」,並選擇「晚餐」表中的「DinnerID」列作為主鍵。 我們的 RSVP 表將是外鍵表和 RSVP。DinnerID 列將作為外鍵關聯:

![](create-a-database/_static/image15.png)

現在,RSVP 表中的每一行都將與"晚餐"表中的一行相關聯。 SQL Server 將為我們保持參考完整性 , 並且阻止我們添加新的 RSVP 行,如果它不指向有效的 Dinner 行。 如果仍有 RSVP 行引用它,它也會阻止我們刪除 Dinner 行。

### <a name="adding-data-to-our-tables"></a>新增資料到我們的表格

最後,讓我們向「晚餐」表添加一些示例數據。 我們可以在伺服器資源管理器中右鍵按一下資料並選擇「顯示表資料」命令,將資料新增到表中:

![](create-a-database/_static/image16.png)

我們將添加幾行 Dinner 數據,稍後在開始實現應用程式時可以使用這些數據:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>後續步驟

我們已經完成了資料庫的創建。 現在,讓我們創建模型類,可用於查詢和更新它。

> [!div class="step-by-step"]
> [前一個](create-a-new-aspnet-mvc-project.md)
> [下一個](build-a-model-with-business-rule-validations.md)
