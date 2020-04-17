---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用實體框架 (C#) 建立模型類 |微軟文件
author: rick-anderson
description: 在本教學中,您將瞭解如何將ASP.NETMVC與Microsoft實體框架一起使用。 您將瞭解如何使用實體精靈建立ADO.NET實體 Da...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 716d34167258b1005b25b1cd11bfaa6d80763320
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542660"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>使用 Entity Framework 建立模型類別 (C#)

由[微軟](https://github.com/microsoft)

> 在本教學中,您將瞭解如何將ASP.NETMVC與Microsoft實體框架一起使用。 您將瞭解如何使用實體嚮導創建ADO.NET實體資料模型。 在本教學中,我們將建構一個 Web 應用程式,說明如何使用實體框架選擇、插入、更新和刪除資料庫資料。

本教學的目的是說明如何在建構ASP.NET MVC 應用程式時使用Microsoft實體架構創建資料存取類。 本教程假定之前對 Microsoft 實體框架沒有瞭解。 在本教學結束時,您將瞭解如何使用實體框架來選擇、插入、更新和刪除資料庫記錄。

Microsoft 實體框架是一個對象關係映射 (O/RM) 工具,使您能夠從資料庫自動生成數據存取層。 實體框架使您能夠避免手動構建數據訪問類的繁瑣工作。

為了說明如何使用微軟實體框架進行ASP.NET MVC,我們將構建一個簡單的示例應用程式。 我們將創建一個影片資料庫應用程式,使您能夠顯示和編輯影片資料庫記錄。

本教程假定您擁有 Visual Studio 2008 或帶 Service Pack 1 的可視化 Web 開發人員 2008。 您需要服務包 1 才能使用實體框架。 您可以透過以下位址下載 Visual Studio 2008 服務套件 1 或帶服務套件 1 的視覺化 Web 開發人員:

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC 和 Microsoft 實體框架之間沒有基本聯繫。 實體框架有幾個替代方法可用於mVCASP.NET。 例如,您可以使用其他 O/RM 工具(如 Microsoft LINQ 到 SQL、NHibernate 或 SubSonic)構建 MVC 模型類。

## <a name="creating-the-movie-sample-database"></a>建立影片範例資料庫

影片資料庫應用程式使用名為「Movie」的資料庫表,其中包含以下列:

| 資料行名稱 | 資料類型 | 允許 Nulls? | 是主鍵嗎? |
| --- | --- | --- | --- |
| Id | int | False | True |
| Title | 恩瓦爾查爾 (100) | False | False |
| 導演 | 恩瓦爾查爾 (100) | False | False |

您可以按照以下步驟將此表加入ASP.NET MVC 專案中:

1. 右鍵按一下「\_解決方案資源管理器」視窗中的應用數據資料夾,然後選擇選單選項 **「添加,新建專案」。。**
2. 在 **「新增新項目」** 對話方塊中,選擇**SQL Server 資料庫**,為資料庫指定名稱 MoviesDB.mdf,然後按下「**添加**」按鈕。
3. 按兩下 MoviesDB.mdf 檔以打開伺服器資源管理器/資料庫資源管理器視窗。
4. 展開 MoviesDB.mdf 資料庫連接,右鍵單擊「表」資料夾,然後選擇功能表選項 **「添加新錶**」。
5. 在表設計器中,添加 Id、標題和控制器列。
6. 按下 **「儲存**」按鈕(它有軟盤的圖示)以儲存新錶的名稱「電影」。。

創建"影片"資料庫表後,應向該表添加一些範例資料。 右鍵按一下「影片」表併選擇功能表選項 **「顯示表數據**」。 您可以將假影片數據輸入顯示的網格中。

## <a name="creating-the-adonet-entity-data-model"></a>建立ADO.NET實體資料模型

為了使用實體框架,您需要創建實體數據模型。 您可以使用視覺化工作室*實體資料模型精靈*從資料庫自動生成實體資料模型。

請遵循下列步驟：

1. 右鍵按一下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇選單選項 **「添加,新專案**」。
2. 在「**添加新專案」** 對話方塊中,選擇「資料」類別(參見圖 1)。
3. 選擇**ADO.NET 實體資料模型**樣本,為實體數據模型指定名稱「電影 DBModel.edmx」,然後按下 **「添加**」按鈕。 按下 **「添加**」按鈕將啟動「數據模型精靈」。
4. 在 **「選擇模型內容」** 步驟中,選擇「**從資料庫產生**」選項,然後單擊 **「下一步**」按鈕(參見圖 2)。
5. 在 **「選擇數據連接**」步驟中,選擇 MoviesDB.mdf 資料庫連接,輸入實體連接設置名稱「電影 DB 實體」,然後單擊 **「下一步**」按鈕(參見圖 3)。
6. 在 **「選擇資料庫物件**」步驟中,選擇「影片資料庫」表並單擊 **「完成」** 按鈕(參見圖 4)。

完成這些步驟後,將打開ADO.NET實體數據模型設計器(實體設計器)。

**圖 1 = 建立新的實體資料模型**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**圖 2 = 選擇模型內容步驟**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**圖 3 = 選擇資料連線**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**圖 4 = 選擇資料庫物件**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>變更ADO.NET實體資料模型

創建實體數據模型后,可以使用實體設計器修改模型(參見圖 5)。 您可以隨時透過雙擊解決方案資源管理器視窗中的「模型」資料夾中的「電影 DBModel.edmx 檔案」來打開實體設計器。

**圖 5 = ADO.NET 實體資料模型設計器**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

例如,可以使用實體設計器更改實體模型數據嚮導生成的類的名稱。 嚮導創建了名為"電影"的新數據存取類。 換句話說,嚮導為類指定與資料庫表相同的名稱。 由於我們將使用此類來表示特定的「影片」實例,因此應將類從「影片」重新命名為「影片」。

如果要重命名實體類,可以按兩下實體設計器中的類名稱並輸入新名稱(參見圖 6)。 或者,您可以在實體設計器中選擇實體后,在"屬性"視窗中更改實體的名稱。

**圖 6 = 變更實體名稱**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

請記住,通過按一下「儲存」按鈕(軟盤的圖示)進行修改後保存實體數據模型。 在後台,實體設計器生成一組C# 類別。 您可以通過從解決方案資源管理器視窗中打開MoviesDBModel.Designer.cs檔來查看這些類。

不要修改Designer.cs檔中的代碼,因為下次使用實體設計器時,您的更改將被覆蓋。 如果要擴充Designer.cs檔案中定義的實體類別的功能,則可以在單獨的檔案中建立*部分類別*。

#### <a name="selecting-database-records-with-the-entity-framework"></a>使用實體框架選擇資料庫記錄

讓我們通過創建顯示影片記錄列表的頁面開始構建影片資料庫應用程式。 清單 1 中的主控制器公開名為 Index() 的操作。 索引() 操作利用實體框架從影片資料庫表中返回所有影片記錄。

**清單1 = 控制器\主控制器.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

請注意,清單 1 中的控制器包括一個構造函數。 建構函數初始化名為\_db 的類級欄位。 db\_欄位表示由Microsoft實體架構生成的資料庫實體。 db\_欄位是實體設計器生成的 MoviesDBEntity 類的實例。

為了在主控制器中使用MoviesDBEntity類,必須導入 MovieEntityApp.models 命名空間 *(MVCProjectName*)。型號)。

db\_欄位在 Index() 操作中使用,以從「影片」資料庫表中檢索記錄。 表達式\_db。MovieSet 表示「影片」資料庫表中的所有記錄。 ToList() 方法用於將影片集轉換為影片物件的泛型集合(&lt;清單 影片&gt;)。

影片記錄在 LINQ 到實體的幫助下檢索。 清單 1 中的 Index() 操作使用 LINQ*方法語法*來檢索資料庫記錄集。 如果您願意,可以使用 LINQ*查詢文法*。 以下兩個語句執行相同的操作:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

使用您認為最直觀的 LINQ 語法(方法語法或查詢語法)。 這兩種方法在性能上沒有差別 ,唯一的區別是風格。

清單 2 中的檢視用於顯示影片記錄。

**清單 2 = 檢視\home_Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

清單 2 中的檢視包含一個**foreach**迴圈,該迴圈迴圈迴圈遍曆每個影片記錄並顯示影片記錄的標題和導演屬性的值。 請注意,每個記錄旁邊都會顯示"編輯"和"刪除"連結。 此外,檢視底部還顯示「添加影片」連結(參見圖 7)。

**圖 7 = 索引檢視**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

索引檢視是*鍵入的檢視*。 索引檢視&lt;包括一個 %@&gt; Page % 指令,該指令具有*繼承*屬性,該屬性將模型屬性轉換&lt;為影片物件(清單影片)的強力類型泛型清單集合。

## <a name="inserting-database-records-with-the-entity-framework"></a>將資料庫記錄插入實體框架

您可以使用實體框架輕鬆將新記錄插入到資料庫表中。 清單3包含添加到主控制器類的兩個新操作,可用於將新記錄插入到 Movie 資料庫表中。

**清單3 = 控制器\主控制器.cs(新增方法)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

第一個 Add() 操作僅返回檢視。 該檢視包含用於添加新影片資料庫記錄的窗體(參見圖 8)。 提交表單時,將調用第二個 Add() 操作。

請注意,第二個 Add() 操作用 AcceptVerbs 屬性進行修飾。 僅當執行 HTTP POST 操作時,才能呼叫此操作。 換句話說,此操作只能在發佈 HTML 窗體時調用。

第二個 Add() 操作在 ASP.NET MVC TryUpdateModel() 方法的幫助下創建實體框架影片類的新實例。 TryUpdateModel() 方法獲取傳遞給 Add() 方法的窗體集合中的欄位,並將這些 HTML 表單欄位的值分配給 Movie 類。

使用實體框架時,在使用 TryUpdateModel 或 UpdateModel 方法更新實體類的屬性時,必須提供屬性的「白名單」。

接下來,Add() 操作執行一些簡單的表單驗證。 該操作驗證"標題"和"控制器"屬性是否具有值。 如果存在驗證錯誤,則會向 ModelState 添加驗證錯誤消息。

如果沒有驗證錯誤,則在實體框架的説明下,將新的影片記錄添加到「電影」資料庫表。 新記錄將新增到資料庫中,並帶有以下兩行代碼:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

第一行代碼將新的影片實體添加到實體框架正在跟蹤的影片集中。 第二行代碼將保存對被跟蹤回基礎資料庫的"電影"所做的任何更改。

**圖 8 = 新增檢視**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>使用實體框架更新資料庫記錄

您可以採用幾乎相同的方法,使用實體框架編輯資料庫記錄,就像我們剛才採用的方法插入新的資料庫記錄一樣。 清單4包含兩個名為 Edit() 的新控制器操作。 第一個 Edit() 操作傳回用於編輯影片記錄的 HTML 窗體。 第二個 Edit() 操作嘗試更新資料庫。

**清單4 = 控制器\主控制器.cs(編輯方法)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

第二個 Edit() 操作首先從與正在編輯的影片的 ID 匹配的資料庫檢索影片記錄。 以下 LINQ 到實體語片取得與特定 Id 符合的第一個資料庫紀錄:

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

接下來,TryUpdateModel() 方法用於將 HTML 表單欄位的值分配給影片實體的屬性。 請注意,提供了一個白名單,以指定要更新的確切屬性。

接下來,執行一些簡單的驗證,以驗證影片標題和導演屬性是否具有值。 如果任一屬性缺少值,則驗證錯誤消息將添加到 ModelState 和 ModelState。IsValid 返回該值為 false。

最後,如果沒有驗證錯誤,則通過調用 SaveChanges() 方法,將更新基礎「電影」資料庫表與任何更改。

編輯資料庫記錄時,需要將正在編輯的記錄的 Id 傳遞給執行資料庫更新的控制器操作。 否則,控制器操作將不知道要在基礎資料庫中更新哪個記錄。 清單 5 中包含的「編輯」檢視包含隱藏表單欄位,該欄位表示要編輯的資料庫記錄的識別碼。

**清單5 = 檢視\home_編輯.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>使用實體框架移除資料庫記錄

本教學中需要處理的最終資料庫操作是刪除資料庫記錄。 您可以使用清單 6 中的控制器操作刪除特定的資料庫記錄。

**清單6 -- [控制器]主控制器.cs(刪除操作)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete() 操作首先檢索與傳遞給該操作的 ID 匹配的 Movie 實體。 接下來,通過調用 DeleteObject() 方法後跟 SaveChanges() 方法從資料庫中刪除影片。 最後,使用者被重定向回索引視圖。

## <a name="summary"></a>總結

本教學的目的是展示如何利用ASP.NET MVC 和Microsoft 實體架構建構資料庫驅動的 Web 應用程式。 您學習了如何建構應用程式,讓您能夠選擇、插入、更新和刪除資料庫記錄。

首先,我們討論了如何使用實體數據模型嚮導從 Visual Studio 中生成實體數據模型。 接下來,您將學習如何使用 LINQ 到實體從資料庫表中檢索一組資料庫記錄。 最後,我們使用實體框架插入、更新和刪除資料庫記錄。

> [!div class="step-by-step"]
> [下一步](creating-model-classes-with-linq-to-sql-cs.md)
