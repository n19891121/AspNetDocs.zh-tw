---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 反覆運算#1 = 建立應用程式 (VB) |微軟文件
author: rick-anderson
description: 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們增加了對基本資料庫操作的支援:創建、讀取、更新和 D...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542530"
---
# <a name="iteration-1--create-the-application-vb"></a>反覆項目 #1 – 建立應用程式 (VB)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>建構 MVC 應用程式 (VB) ASP.NET連絡人管理

在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。 透過聯絡人管理員應用程式,您可以儲存連絡人資訊 (姓名、電話號碼和電子郵件位址) 人員清單。

我們通過多次反覆運算構建應用程式。 每次反覆運算時,我們都會逐步改進應用程式。 此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。

- 反覆運算#1 - 創建應用程式。 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。

- 反覆運算#2 - 使應用程式看起來不錯。 在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。

- 反覆運算#3 - 添加表單驗證。 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證電子郵件地址和電話號碼。

- 反覆運算#4 - 使應用程式鬆散耦合。 在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。 例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。

- 反覆運算#5 - 創建單元測試。 在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。 我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。

- 反覆運算#6 - 使用測試驅動開發。 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,我們添加聯繫人組。

- 反覆運算#7 - 添加Ajax功能。 在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。

## <a name="this-iteration"></a>此反覆運算

在第一次反覆運算中,我們將構建基本應用程式。 目標是以最快、最簡單的方式構建聯繫人管理器。 在以後的反覆運算中,我們改進了應用程式的設計。

聯繫人管理器應用程式是一個基本的資料庫驅動應用程式。 您可以使用該應用程式創建新連絡人、編輯現有連絡人和刪除連絡人。

在此反覆運算中,我們完成以下步驟:

1. ASP.NET MVC 應用程式
2. 建立資料庫以儲存我們的聯絡人
3. 使用 Microsoft 實體架構為資料庫產生模型類別
4. 建立控制器操作與檢視,讓我們能夠列出資料庫中的所有聯絡人
5. 建立控制器操作與檢視,讓我們能夠建立新聯絡人
6. 建立控制器操作與檢視,讓我們可以編輯資料庫中的現有聯絡人
7. 建立控制器操作與檢視,讓我們能夠移除資料庫中的現有聯絡人

## <a name="software-prerequisites"></a>軟體必要條件

在ASP.NET MVC 應用程式中,必須在您的電腦上安裝 Visual Studio 2008 或 Visual Web 開發人員 2008(可視化 Web 開發人員是 Visual Studio 的免費版本,不包含 Visual Studio 的所有高級功能)。 您可以透過以下位址下載 Visual Studio 2008 試用版或視覺化 Web 開發人員版本:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 對於具有視覺化 Web 開發人員 ASP.NET MVC 應用程式,必須安裝可視化 Web 開發人員服務包 1。 如果沒有服務包 1,則無法創建 Web 應用程式專案。

ASP.NET MVC 框架。 可以從以下位址下載ASP.NET MVC 框架:

[https://www.asp.net/mvc](../../../index.md)

在本教學中,我們使用Microsoft實體框架訪問資料庫。 實體框架包含在 .NET 框架 3.5 服務包 1 中。 您可以透過以下位置下載此服務套件:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d斯普拉朗](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

作為逐個執行每個下載的替代方法,您可以利用 Web 平臺安裝程式 (Web PI)。 您可以透過以下位址下載 Web PI:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 專案

ASP.NET MVC Web 應用程式專案。 啟動視覺化工作室並選擇選單選項**檔案,新專案**。 將顯示 **「新專案」** 對話框(參見圖 1)。 選擇**Web**專案類型和**ASP.NET MVC Web 應用程式**樣本。 說出您的新項目*聯繫人管理器*,然後按下"確定"按鈕。

請確保從 **「新專案」** 對話框右上角的下拉清單中選擇了 .NET Framework 3.5。 否則,將不會顯示ASP.NET MVC Web 應用程式範本。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)

**圖 01**: 新的項目對話框([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image2.png))

ASP.NET MVC 應用程式,將顯示 **「創建單元測試項目**」對話方塊。 可以使用此對話方塊指示在創建ASP.NET MVC 應用程式時要創建單元測試專案並將其添加到解決方案中。 儘管我們在此反覆運算中不會構建單元測試,但應選擇選項 **「是」,創建單元測試專案**,因為我們計劃在以後的反覆運算中添加單元測試。 首次創建新的ASP.NET MVC 專案時添加測試專案比創建ASP.NET MVC 專案後添加測試專案要容易得多。

> [!NOTE] 
> 
> 由於視覺化 Web 開發人員不支援測試專案,因此在使用可視化 Web 開發人員時,您不會獲取「創建單元測試專案」 對話框。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)

**圖 02**: 建立單元測試項目對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image4.png))

ASP.NET MVC 應用程式顯示在可視化工作室解決方案資源管理器視窗中(參見圖 3)。 如果看不到"解決方案資源管理器"視窗,則可以通過選擇功能表選項 **"視圖"、"解決方案資源管理員**"來打開此視窗。 請注意,該解決方案包含兩個專案:ASP.NET MVC 專案和測試專案。 mVCASP.NET專案命名為"連絡人管理器",測試專案命名為"連絡人管理器"。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)

**圖 03**: 解決方案資源管理員視窗 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>刪除項目範例檔案

ASP.NET MVC 專案範本包括控制器和檢視的範例檔。 在創建新ASP.NET MVC 應用程式之前,應刪除這些檔。 您可以通過右鍵單擊檔或資料夾並選擇功能表選項 **「刪除**」來刪除解決方案資源管理器視窗中的檔案和資料夾。

您需要從 ASP.NET MVC 項目中移除以下檔案:

- [控制器]主控制器.vb

- [視圖]主頁\關於.aspx

- [視圖]主頁\索引.aspx

而且,您需要從測試項目中刪除以下檔:

[控制器]主控制器測試.vb

## <a name="creating-the-database"></a>建立資料庫

連絡人管理員應用程式是資料庫驅動的 Web 應用程式。 我們使用資料庫來存儲聯繫資訊。

ASP.NET MVC 框架,包含任何現代資料庫,包括 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 資料庫。 在本教學中,我們使用Microsoft SQL Server資料庫。 安裝 Visual Studio 時,系統會提供安裝 Microsoft SQL Server Express 的選項,這是 Microsoft SQL Server 資料庫的免費版本。

通過右鍵單擊解決方案資源管理器視窗中的應用\_資料資料夾並選擇功能表選項 **「添加、新專案**」來創建新資料庫。 在 **「新增新項目」** 對話方塊中,選擇 **「資料**」類別和**SQL Server 資料庫**樣本(參見圖 4)。 命名新資料庫 ContactManagerDB.mdf,然後單擊"確定"按鈕。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)

**圖04**:建立新的微軟 SQL Server Express 資料庫 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image8.png))

創建新資料庫後,資料庫將顯示在解決方案資源管理器視窗中的應用\_資料資料夾中。 按兩下 ContactManager.mdf 檔案以開啟伺服器資源管理員視窗並連接到資料庫。

> [!NOTE] 
> 
> 伺服器資源管理員窗口稱為資料庫資源管理員視窗(對於Microsoft視覺化Web開發人員)。

可以使用 Server 資源管理器視窗創建新的資料庫物件,如資料庫表、視圖、觸發器和儲存過程。 右鍵按下「表」資料夾並選擇功能表選項 **「新增新表**」。。 將顯示資料庫表設計器(參見圖 5)。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)

**圖 05**: 資料庫表設計器 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image10.png))

我們需要建立以下欄的表格:

<a id="0.2_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| Id | int | false |
| 名字 | nvarchar(50) | false |
| 姓氏 | nvarchar(50) | false |
| 電話 | nvarchar(50) | false |
| 電子郵件 | nvarchar(255) | false |

第一列"Id"列是特殊的。 您需要將 Id 列標記為識別列和主鍵列。 通過展開列屬性(查看圖 6 的底部)向下滾動到標識規範屬性,指示列是標識列。 將 **(是識別)** 屬性設定為值**是**。

通過選擇列並按一下帶有鍵圖示的按鈕,將列標記為主鍵列。 將列標記為主鍵列后,列旁邊將顯示一個鍵圖示(參見圖 6)。

完成表創建後,按下「儲存」按鈕(帶有軟盤圖示的按鈕)以保存新錶。 為您的新表命名 *「連絡人*」。

完成創建"連絡人"資料庫表後,應向該表添加一些記錄。 右鍵按一下伺服器資源管理器視窗中的"連絡人"表,然後選擇功能表選項 **"顯示表資料**"。 在顯示的網格中輸入一個或多個聯繫人。

## <a name="creating-the-data-model"></a>建立資料模型

ASP.NET MVC 應用程式由模型、視圖和控制器組成。 我們首先創建一個模型類,該類表示我們在上一節中創建的"連絡人"表。

在本教學中,我們使用Microsoft實體框架從資料庫自動生成模型類。

> [!NOTE] 
> 
> ASP.NET MVC 框架不以任何方式綁定到 Microsoft 實體框架。 您可以將mVCASP.NET替代資料庫存取技術(包括 NHibernate、LINQ 到 SQL 或ADO.NET) 使用。

依以下步驟建立資料模型類別:

1. 右鍵按下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇「**添加新專案**」。 將顯示 **「添加新專案」** 對話框(參見圖 6)。
2. 選擇 **「資料**」類別和**ADO.NET 實體資料模型**樣本。 命名資料模型*ContactManagerModel.edmx,* 然後按下 **「添加**」按鈕。 將顯示實體數據模型向導(參見圖 7)。
3. 在 **「選擇模型內容」** 步驟中,選擇**從資料庫中生成**(參見圖 7)。
4. 在 **「選擇資料連線**」步驟中,選擇 ContactManagerDB.mdf 資料庫,並輸入實體連接設定的名稱 *「連絡人管理器資料庫實體*」(參見圖 8)。
5. 在 **「選擇資料庫物件**」步驟中,選擇標記為表的複選框(參見圖 9)。 數據模型將包括資料庫中包含的所有表(只有一個,"連絡人"表)。 輸入命名空間*模型*。 按下「完成」按鈕以完成嚮導。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)

**圖 06**: 新增新項目對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image12.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)

**圖 07**: 選擇模型內容 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image14.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)

**圖 08**: 選擇您的資料連線 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image16.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)

**圖 09**: 選擇資料庫物件([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image18.png))

完成實體數據模型嚮導後,將顯示實體數據模型設計器。 設計器顯示與要建模的每個表對應的類。 您應該會看到一個名為"連絡人"的類。

實體數據模型向導基於資料庫表名稱生成類名稱。 您幾乎總是需要更改精靈產生的類的名稱。 右鍵單擊設計器中的"連絡人"類,然後選擇功能表選項 **"重新命名**。 將類的名稱從"連絡人"(複數)更改為"連絡人"(單數)。 更改類名稱后,類應如下所示 10。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)

**圖10**: 連絡人類 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image20.png))

此時,我們創建了資料庫模型。 我們可以使用 Contact 類來表示資料庫中的特定聯繫人記錄。

## <a name="creating-the-home-controller"></a>建立主控制器

下一步是創建我們的主控制器。 主控制器是在 mVC 應用程式中調用的預設控制器 ASP.NET。

通過右鍵單擊解決方案資源管理器視窗中的控制器資料夾並選擇功能表選項 **「添加,控制器**」(參見圖 11),創建主控制器類。 請注意,標記為「**添加創建、更新和詳細資訊方案」操作方法的**複選框。 在按下「**添加**」按鈕之前,請確保選中此複選框。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)

**圖11**: 新增主控制器 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image22.png))

建立主控制器時,您將獲得清單 1 中的類。

**清單1 - 控制器\主控制器.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a>列出聯絡人

為了在"連絡人"資料庫表中顯示記錄,我們需要創建一個索引() 操作和索引視圖。

主控制器已包含索引() 操作。 我們需要修改此方法,以便它看起來像清單 2。

**清單2 - 控制器\主控制器.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

請注意,清單 2 中的主控制器類\_包含名為 實體的專用欄位。 實體\_欄位表示數據模型中的實體。 我們使用\_實體欄位與資料庫通信。

Index() 方法傳回表示連絡人資料庫表中的所有聯繫人的檢視。 表達式\_實體。連絡人集.ToList() 將連絡人清單作為通用清單返回。

現在,我們已經創建了索引控制器,接下來我們需要創建索引視圖。 在創建索引檢視之前,請透過選擇功能表選項 **「生成、生成解決方案**」來編譯應用程式。 在添加檢視之前,應始終編譯專案,以便在 **「添加檢視**」對話框中顯示模型類清單。

通過右鍵單擊 Index() 方法並選擇選單選項 **「添加檢視**」來建立索引檢視(請參見圖 12)。 選擇此選單選項將打開 **「添加檢視」** 對話框(參見圖 13)。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)

**圖 12**: 新增索引檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image24.png))

在 **'新增檢視'** 對話框中, 選擇標籤為「**建立強類型檢視」 選單的欄位**。 選擇「查看數據類聯繫人管理器.連絡人」 和「查看內容清單」。 選擇這些選項將生成顯示聯繫人記錄列表的檢視。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)

**圖 13**: 新增檢視對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image26.png))

按下「**添加**」按鈕時,將生成清單 3 中的索引檢視。 請注意&lt;顯示在檔案頂部&gt;的 %@ 頁 % 指令。 &lt;索引檢視從ViewPage IE500"&lt;聯繫人管理器.模型.連&gt;&gt;絡人 類繼承。 換句話說,視圖中的 Model 類表示聯繫人實體的清單。

Index 檢視的正文包含一個 foreach 迴圈,該迴圈通過模型類表示的每個聯繫人進行迴圈。 Contact 類別的每個屬性的值顯示在 HTML 表中。

**清單 3 - 檢視\home_Index.aspx(未修改)**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

我們需要對索引視圖進行一次修改。 由於我們不是在創建"詳細資訊"視圖,因此我們可以刪除"詳細資訊"連結。 從索引檢視尋找與移除以下代碼:

{.id = 項。Id=)%&gt;

修改索引檢視後,可以運行聯繫人管理器應用程式。 選擇功能表選項「調試」、「開始調試」或「按 F5」。 首次運行應用程式時,您將獲得圖 14 中的對話方塊。 選擇 **「修改 Web.config 檔以啟用除錯**」選項,然後單擊「確定」 按鈕。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)

**圖14**:啟用除錯 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image28.png))

默認情況下,將返回索引視圖。 此檢視列出聯繫人資料庫表中的所有數據(參見圖 15)。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)

**圖 15**: 索引檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image30.png))

請注意,索引檢視在視圖底部包含標記為"新建"的連結。 在下一節中,您將瞭解如何創建新聯繫人。

## <a name="creating-new-contacts"></a>建立新連絡人

為了使用戶能夠創建新的聯繫人,我們需要向主控制器添加兩個 Create() 操作。 我們需要創建一個 Create() 操作,該操作傳回 HTML 表單以創建新連絡人。 我們需要創建第二個 Create() 操作,以執行新聯繫人的實際資料庫插入。

我們需要添加到主控制器的新 Create() 方法包含在清單 4 中。

**清單4 - 控制器\homeController.vb(使用建立方法)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

第一個 Create() 方法可以使用 HTTP GET 調用,而第二個 Create() 方法只能由 HTTP POST 調用。 換句話說,第二個 Create() 方法只能在發表 HTML 窗體時調用。 第一個 Create() 方法僅傳回包含用於創建新連絡人的 HTML 窗體的檢視。 第二個 Create() 方法更有趣:它將新的聯繫人添加到資料庫中。

請注意,已修改第二個 Create() 方法以接受 Contact 類的實例。 從 HTML 窗體發佈的表單值由 ASP.NET MVC 框架自動綁定到此 Contact 類。 HTML 創建表單中的每個表單欄位都分配給聯絡人「參數的屬性。

請注意,連絡人參數用 [Bind] 屬性進行修飾。 [綁定] 屬性用於從綁定中排除聯繫人 Id 屬性。 由於 Id 屬性表示標識屬性,因此我們不希望設置 Id 屬性。

在 Create() 方法的正文中,實體框架用於將新的聯繫人插入到資料庫中。 新的連絡人將添加到現有的連絡人集,並調用 SaveChanges() 方法將這些更改推送回基礎資料庫。

您可以通過右鍵按兩個 Create() 方法之一併選擇選單選項 **「新增檢視**」來生成用於創建新聯繫人的 HTML 表單(參見圖 16)。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)

**圖 16**: 新增建立檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image32.png))

在 **「添加檢視」** 對話方塊中,選擇 **「連絡人管理員.連絡人」** 類別和「建立檢視內容 **」** 選項(參見圖 17)。 按下「**添加**」按鈕時,將自動生成"創建"檢視。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)

**圖17**: 看到頁面爆炸 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image34.png))

"創建"檢視包含 Contact 類的每個屬性的表單欄位。 "創建"檢視的代碼包含在清單 5 中。

**清單 5 - 檢視\home_Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

修改 Create() 方法並添加"創建"視圖後,可以運行連絡人經理應用程式並創建新連絡人。 按下「**新建**」檢視中顯示的連結以導航到「創建」檢視。 您應該在圖 18 中看到檢視。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)

**圖 18**: 建立檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image36.png))

## <a name="editing-contacts"></a>編輯聯絡人

添加用於編輯連絡人記錄的功能與添加創建新連絡人記錄的功能非常相似。 首先,我們需要向主控制器類添加兩種新的 Edit 方法。 這些新的 Edit() 方法包含在清單 6 中。

**清單6 - 控制器\主控制器.vb(使用編輯方法)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

第一個 Edit() 方法由 HTTP GET 操作調用。 Id 參數傳遞給此方法,此方法表示要編輯的聯繫人記錄的 ID。 實體框架用於檢索與 Id 匹配的連絡人。返回包含用於編輯記錄的 HTML 窗體的檢視。

第二個 Edit() 方法執行對資料庫的實際更新。 此方法接受 Contact 類的實例作為參數。 ASP.NET MVC 框架會自動將表單欄位從「編輯」窗體綁定到此類。 請注意,在編輯連絡人時,您沒有包含 [Bind] 屬性(我們需要 Id 屬性的值)。

實體框架用於將修改後的聯繫人保存到資料庫。 必須首先從資料庫中檢索原始聯繫人。 接下來,調用實體框架應用屬性更改() 方法來記錄對聯繫人的更改。 最後,調用實體框架保存更改() 方法來保留對基礎資料庫的更改。

您可以通過右鍵按一下 Edit() 方法並選擇選單選項「添加檢視」來生成包含「編輯」窗體的視圖。 在"添加檢視"對話框中,選擇 **"連絡人管理器.模型.聯繫人類"** 和 **「編輯**檢視」內容(參見圖 19)。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)

**圖 19**: 新增編輯檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image38.png))

按下「添加」按鈕時,將自動生成新的「編輯」檢視。 生成的 HTML 窗體包含對應於 Contact 類的每個屬性的欄位(請參見清單 7)。

**清單7 - 檢視\home_編輯.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>移除聯絡人

如果要刪除連絡人,則需要向主控制器類添加兩個 Delete() 操作。 第一個刪除() 操作顯示刪除確認表單。 第二個 Delete() 操作執行實際刪除。

> [!NOTE] 
> 
> 稍後,在反覆運算#7中,我們修改聯繫人管理器,以便它支援 Ajax 刪除的一個步驟。

清單8中包含兩種新的 Delete() 方法。

**清單8 - 控制器\主控制器.vb(刪除方法)**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

第一個 Delete() 方法傳回一個確認表單,用於從資料庫中刪除連絡人記錄(參見圖 20)。 第二個 Delete() 方法對資料庫執行實際刪除操作。 從資料庫檢索原始連絡人後,將調用實體框架 DeleteObject() 和保存更改()方法以執行資料庫刪除。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)

**圖20**:刪除確認檢視([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image40.png))

我們需要修改 Index 檢視,以便它包含用於刪除聯繫人記錄的連結(參見圖 21)。 您需要將以下代碼加入包含「編輯」連結的同一表單元格中:

{.id = 項。Id=)%&gt;

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)

**圖21**:索引檢視與編輯連結([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image42.png))

接下來,我們需要創建刪除確認檢視。 右鍵按一下主控制器類中的 Delete() 方法,然後選擇選單選項「添加視圖」。 將顯示「添加檢視」對話框(參見圖 22)。

與「清單」、"創建「和」編輯「檢視」的情況不同,「添加檢視」對話框不包含創建「刪除」檢視的選項。 而是選擇 **「聯繫人管理器.模型.連絡人**資料類」和 **「空**檢視」內容。 選擇"空檢視內容"選項需要我們自己創建視圖。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)

**圖22**:新增刪除確認檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image44.png))

"刪除"檢視的內容包含在清單 9 中。 此檢視包含一個表單,該窗體確認是否應刪除特定聯繫人(參見圖 21)。

**清單 9 - 檢視\home_Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>變更預設控制器名稱

使用聯絡人的控制器類的名稱名為 HomeController 類,這可能會讓您煩惱。 控制器不應被命名為「連絡人控制器」?

此問題很容易解決。 首先,我們需要重構主控制器的名稱。 在 Visual Studio 代碼編輯器中打開 HomeController 類,右鍵單擊類的名稱並選擇選單選項 **「重命名**」。 選擇此選單選項將打開" 重新命名對話框。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)

**圖23**:重構控制器名稱 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image46.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)

**圖24**:使用重新命名對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image48.png))

如果重新命名控制器類,Visual Studio 也會更新「檢視」資料夾中資料夾的名稱。 Visual Studio 會將 [視圖]主頁資料夾重命名為 [視圖]連絡人資料夾。

進行此更改後,應用程式將不再具有主控制器。 執行應用程式時,您將獲得圖 25 中的錯誤頁。

[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)

**圖25:** 無預設控制器([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image50.png))

我們需要更新 Global.asax 檔案中的預設路由,以便使用聯繫人控制器而不是主控制器。 打開 Global.asax 檔並修改預設路由使用的預設控制器(請參見清單 10)。

**清單10 - 全域.asax.vb**

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

進行這些更改後,聯繫人管理器將正確運行。 現在,它將使用聯繫人控制器類作為默認控制器。

## <a name="summary"></a>總結

在第一次反覆運算中,我們以盡可能快的方式創建了一個基本的聯繫人管理器應用程式。 我們利用 Visual Studio 自動為控制器和檢視生成初始代碼。 我們還利用實體框架自動生成資料庫模型類。

目前,我們可以使用聯繫人管理器應用程式列出、創建、編輯和刪除聯繫人記錄。 換句話說,我們可以執行資料庫驅動的 Web 應用程式所需的所有基本資料庫操作。

不幸的是,我們的應用程式有一些問題。 首先,我猶豫地承認這一點,聯繫人管理器應用程式不是最有吸引力的應用程式。 它需要一些設計工作。 在下一次反覆運算中,我們將瞭解如何更改默認視圖母版頁和級聯樣式表,以改善應用程序的外觀。

其次,我們尚未實現任何表單驗證。 例如,沒有任何措施可以阻止您提交"創建連絡人表單",而無需為任何表單欄位輸入值。 此外,您還可以輸入無效的電話號碼和電子郵寄地址。 我們開始在反覆運算#3解決表單驗證問題。

最後,最重要的是,無法輕鬆修改或維護聯繫人管理器應用程式的當前反覆運算。 例如,資料庫訪問邏輯直接烘焙到控制器操作中。 這意味著,如果不修改控制器,我們就無法修改數據訪問代碼。 在以後的反覆運算中,我們探索了可以實現的軟體設計模式,以使聯繫人管理器對更改更具彈性。

> [!div class="step-by-step"]
> [前一個](iteration-7-add-ajax-functionality-cs.md)
> [下一個](iteration-2-make-the-application-look-nice-vb.md)
