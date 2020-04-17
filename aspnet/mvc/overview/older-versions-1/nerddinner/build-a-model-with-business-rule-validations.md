---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 使用業務規則驗證建構模型 |微軟文件
author: rick-anderson
description: 步驟 3 演示如何創建模型,可用於查詢和更新 NerdDinner 應用程式的資料庫。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 1a316e9051cf56cd4f1546336b334ace991c05b3
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541633"
---
# <a name="build-a-model-with-business-rule-validations"></a>使用商務規則驗證建置模型

由[微軟](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第3步,該教程示範如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。
> 
> 步驟 3 演示如何創建模型,可用於查詢和更新 NerdDinner 應用程式的資料庫。
> 
> 如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。

## <a name="nerddinner-step-3-building-the-model"></a>神經晚餐步驟 3: 構建模型

在模型檢視控制器框架中,術語"模型"是指表示應用程序數據的物件,以及與其集成驗證和業務規則的相應域邏輯。 該模型在許多方面是基於 MVC 的應用程式的「心臟」,稍後我們將看到從根本上推動它的行為。

ASP.NET MVC 框架支援使用任何資料存取技術,開發人員可以從各種豐富的 .NET 資料選項中進行選擇以實施其模型,包括:LINQ 到實體、LINQ 到 SQL、NHibernate、LLBLGen Pro、SubSonic、WilsonORM,或者只是原始ADO.NET數據閱讀器或數據集集。

對於我們的NerdDinner應用程式,我們將使用LINQ到SQL來創建一個與資料庫設計相當一致的簡單模型,並添加一些自定義驗證邏輯和業務規則。 然後,我們將實現一個存儲庫類,該類可説明從應用程式的其餘部分提取數據持久性實現,並使我們能夠輕鬆地對其進行單元測試。

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ 到 SQL 是作為 .NET 3.5 的一部分而附帶的 ORM(對象關係映射器)。

LINQ 到 SQL 提供了一種將資料庫表映射到 .NET 類的簡單方法,我們可以針對它編寫代碼。 對於我們的NerdDinner應用程式,我們將用它來將資料庫中的晚餐和RSVP表映射到晚餐和RSVP類。 晚餐和 RSVP 表的列將對應於「晚餐」和「RSVP」類的屬性。 每個 Dinner 和 RSVP 物件將表示資料庫中的 Dinner 或 RSVP 表中的單獨行。

LINQ 到 SQL 允許我們避免手動構造 SQL 語句來檢索和更新具有資料庫數據的 Dinner 和 RSVP 物件。 相反,我們將定義 Dinner 和 RSVP 類、它們如何映射到/從資料庫映射以及它們之間的關係。 然後,LINQ到 SQL 將負責生成適當的 SQL 執行邏輯,以便在運行時交互使用它們時使用。

我們可以在VB和C#中使用LINQ語言支援來編寫表達性查詢,從資料庫中檢索Dinner和RSVP物件。 這最大限度地減少了我們需要編寫的數據代碼量,並允許我們構建真正乾淨的應用程式。

### <a name="adding-linq-to-sql-classes-to-our-project"></a>將 LINQ 新增到 SQL 類別到我們的項目

我們將從右鍵單擊專案中的「模型」資料夾開始,然後選擇 **「新增&gt;新 專案**」選單命令:

![](build-a-model-with-business-rule-validations/_static/image1.png)

這將彈出「添加新項目」對話框。 我們將按「資料」類別進行篩選,並在其中選擇「LINQ 到 SQL 類」樣本:

![](build-a-model-with-business-rule-validations/_static/image2.png)

我們將為專案命名為「NerdDinner」,然後單擊「添加」按鈕。 Visual Studio 將在我們的 #Model 目錄下添加 NerdDinner.dbml 檔案,然後打開 LINQ 到 SQL 物件關係設計器:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>使用 LINQ 建立 SQL 的資料模型類別

LINQ 到 SQL 使我們能夠從現有資料庫架構快速創建數據模型類。 為此,我們將在伺服器資源管理器中打開NerdDinner資料庫,並選擇要在其中建模的表:

![](build-a-model-with-business-rule-validations/_static/image4.png)

然後,我們可以將表拖到 LINQ 到 SQL 設計器表面。 當我們執行此操作 LINQ 到 SQL 時,將使用表格架構(具有映射到資料庫表列的類屬性)自動建立 Dinner 和 RSVP 類別:

![](build-a-model-with-business-rule-validations/_static/image5.png)

默認情況下,LINQ到 SQL 設計器在基於資料庫架構創建類時自動「複數」表和列名稱。 例如:我們上面示例中的「Dinners」表產生了一個「Dinner」類。 此類命名有助於使我們的模型與 .NET 命名約定保持一致,我通常發現讓設計器修復這一點很方便(尤其是在添加大量表時)。 但是,如果您不喜歡設計器生成的類或屬性的名稱,則始終可以重寫它並將其更改為所需的任何名稱。 可以通過在設計器內編輯實體/屬性名稱,或通過屬性網格對其進行修改來執行此操作。

默認情況下,LINQ 到 SQL 設計器還會檢查表的主鍵/外鍵關係,並基於這些關係自動在它創建的不同模型類之間創建預設的「關係關聯」。 例如,當我們將 Dinner 和 RSVP 表拖到 LINQ 到 SQL 設計器時,根據 RSVP 表對 Dinners 表具有外鍵(由設計器中的箭頭指示)推斷兩者之間存在一對多關係關聯:

![](build-a-model-with-business-rule-validations/_static/image6.png)

上述關聯將導致 LINQ 到 SQL 向 RSVP 類添加強類型「Dinner」屬性,開發人員可以使用該屬性訪問與給定 RSVP 關聯的 Dinner。 它還會導致 Dinner 類具有" RSVP"集合屬性,使開發人員能夠檢索和更新與特定 Dinner 關聯的 RSVP 物件。

下面您可以看到 Visual Studio 中一個智慧感知示例,當我們創建新的 RSVP 物件並將其添加到 Dinner 的 RSVP 集合中時。 請注意 LINQ 到 SQL 如何在 Dinner 物件上自動新增「RSV」集合:

![](build-a-model-with-business-rule-validations/_static/image7.png)

通過將 RSVP 物件添加到 Dinner 的 RSVP 集合中,我們告訴 LINQ 到 SQL 來關聯資料庫中的 Dinner 和 RSVP 行之間的外鍵關係:

![](build-a-model-with-business-rule-validations/_static/image8.png)

如果您不喜歡設計器建模或命名表關聯的方式,則可以重寫它。 只需單擊設計器中的關聯箭頭,並通過屬性網格訪問其屬性以重命名、刪除或修改它。 但是,對於我們的NerdDinner應用程式,默認關聯規則非常適合我們構建的數據模型類,我們可以只使用默認行為。

### <a name="nerddinnerdatacontext-class"></a>內德晚餐資料上下文類

Visual Studio 將自動建立 .NET 類,這些類表示使用 LINQ 到 SQL 設計器定義的模型和資料庫關係。 還將為添加到解決方案的每個 LINQ 到 SQL 設計器檔生成 LINQ 到 SQL DataContext 類。 由於我們將 LINQ 命名為 SQL 類項「NerdDinner」,因此創建的數據上下文類將稱為「NerdDinnerDataContext」。 此NerdDinnerDataContext類是我們與資料庫互動的主要方式。

我們的NerdDinnerDataContext類公開了兩個屬性 - 'Dinners" 和"RSVPs" - 它們表示我們在資料庫中建模的兩個表。 我們可以使用 C# 針對這些屬性編寫 LINQ 查詢,以便從資料庫中查詢和檢索 Dinner 和 RSVP 物件。

以下代碼演示如何實例化NerdDinnerDataContext物件,並針對該物件執行LINQ查詢,以獲取將來發生的一系列Dinner。 Visual Studio 在編寫 LINQ 查詢時提供完整的無意義,從它返回的對像是強類型,並且還支援智慧感知:

![](build-a-model-with-business-rule-validations/_static/image9.png)

除了允許我們查詢晚餐和RSVP物件外,NerdDinnerDataContext 還會自動跟蹤我們隨後對我們通過它檢索的晚餐和 RSVP 物件所做的任何更改。 我們可以使用此功能輕鬆地將更改保存回資料庫 - 而無需編寫任何顯式 SQL 更新代碼。

例如,下面的程式碼展示如何使用 LINQ 查詢從資料庫中檢索單個 Dinner 物件,更新兩個 Dinner 屬性,然後將更改儲存回資料庫:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

上面代碼中的NerdDinnerDataContext物件自動追蹤我們對從該物件檢索到的Dinner物件所做的屬性更改。 當我們調用"提交更改()"方法時,它將對資料庫執行適當的 SQL"UPDATE"語句,以保留更新的值。

### <a name="creating-a-dinnerrepository-class"></a>建立晚餐儲存庫類別

對於小型應用程式,有時讓控制器直接針對 LINQ 到 SQL DataContext 類工作,並將 LINQ 查詢嵌入到控制器中,這有時很好。 但是,隨著應用程式變得越來越大,此方法在維護和測試方面變得繁瑣起來。 它還可能導致我們在多個位置複製相同的 LINQ 查詢。

使應用程式更易於維護和測試的一種方法是使用"存儲庫"模式。 存儲庫類有助於封裝數據查詢和持久性邏輯,並從應用程式抽象數據持久性的實現詳細資訊。 除了使應用程式代碼更簡潔之外,使用存儲庫模式還可以使將來更輕鬆地更改數據存儲實現,並且它可以説明簡化應用程式單元測試,而無需真正的資料庫。

對於我們的NerdDinner應用程式,我們將定義一個帶有以下簽名的 DinnerRepository 類:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*注意:在本章的後面部分,我們將從此類中提取 IDinnerRepository 介面,並在我們的控制器上啟用依賴項注入。不過,首先,我們將開始簡單,只是直接與 DinnerRepository 類一起工作。*

要實現此類,我們將右鍵單擊我們的"模型"資料夾,然後選擇 **「添加&gt;新專案**」功能表命令。 在「添加新項目」對話框中,我們將選擇「類」樣本並將檔案命名為「DinnerRepository.cs」:

![](build-a-model-with-business-rule-validations/_static/image10.png)

然後,我們可以使用以下代碼實現我們的 DinnerRepository 類:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>使用 DinnerRepository 類別索、更新、插入和刪除

現在,我們已經創建了 DinnerRepository 類,讓我們看一些代碼示例,這些示例演示了我們可以執行的常見任務:

#### <a name="querying-examples"></a>查詢範例

以下代碼使用 DinnerID 值檢索單個晚餐:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

下面的代碼檢索所有即將舉辦的晚餐,並在它們上迴圈:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>插入並更新範例

下面的代碼演示了添加兩個新晚餐。 在調用"Save()"方法之前,不會將存儲庫的添加/修改提交到資料庫。 LINQ 到 SQL 會自動包裝資料庫事務中的所有變更 , 因此,當我們的儲存庫保存時,要麼發生所有更改,要麼這些更改都不會發生:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

下面的代碼檢索現有的 Dinner 物件,並修改其上的兩個屬性。 當我們的儲存庫上調用「Save())」方法時,更改將提交回資料庫:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

下面的代碼檢索晚餐,然後向其中添加 RSVP。 它使用 LINQ 到 SQL 為我們創建的 Dinner 物件上的 RSVP 集合來這樣做(因為資料庫中兩者之間存在主鍵/外鍵關係)。 當在儲存庫上調用「Save())」方法時,此更改將作為新的 RSVP 表行保留回資料庫:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>刪除範例

下面的代碼檢索現有的 Dinner 物件,然後將其標記為要刪除。 在儲存函式庫上調用「Save())」方法時,它將將刪除提交回資料庫:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>將驗證和業務規則邏輯與模型類別

集成驗證和業務規則邏輯是任何處理數據的應用程序的關鍵部分。

#### <a name="schema-validation"></a>結構描述驗證

使用 LINQ 到 SQL 設計器定義模型類時,數據模型類中屬性的數據類型對應於資料庫表的數據類型。 例如:如果 Dinners 表中的「EventDate」列是「日期時間」,則 LINQ 創建的 SQL 資料模型類的類型為「DateTime」(這是內置的 .NET 數據類型)。 這意味著,如果您嘗試從代碼為其分配整數或布爾,則收到編譯錯誤,如果嘗試在運行時隱式將無效字串類型轉換為該字串類型,則會自動引發錯誤。

LINQ 到 SQL 還會在使用字串時自動處理轉義 SQL 值,這有助於在使用字串時防止 SQL 注入攻擊。

#### <a name="validation-and-business-rule-logic"></a>驗證與業務規則邏輯

架構驗證作為第一步非常有用,但很少足夠。 大多數實際方案都需要能夠指定更豐富的驗證邏輯,該驗證邏輯可以跨越多個屬性,執行代碼,並且通常瞭解模型的狀態(例如:它是在創建/更新/刪除,還是處於特定於域的狀態(如"存檔")。 有多種不同的模式和框架可用於定義驗證規則並將其應用於模型類,並且有幾個基於 .NET 的框架可用於幫助實現此。 您可以在mVC應用程式中使用幾乎任何ASP.NET。

為了我們的NerdDinner應用程式,我們將使用相對簡單和直接的模式,在其中我們公開IsValid屬性和GetRule侵犯() 方法在我們的Dinner模型物件上。 IsValid 屬性將返回真或假,具體取決於驗證和業務規則是否都有效。 GetRule違反() 方法將返回任何規則錯誤的清單。

我們將通過在我們的專案中添加「部分類」來實現「有效」和 GetRule 違反()) 我們的晚餐模型。 部分類可用於向 VS 設計器維護的類(如 LINQ 生成的到 SQL 設計器生成的 Dinner 類)添加方法/ 屬性/ 事件,並説明避免工具混亂我們的代碼。 我們可以通過右鍵單擊 #Model 資料夾,將新的部分類添加到專案中,然後選擇"添加新專案"功能表命令。 然後,我們可以在"添加新項目"對話框中選擇"類"範本,並將其命名為Dinner.cs。

![](build-a-model-with-business-rule-validations/_static/image11.png)

按下「添加」按鈕會將Dinner.cs檔添加到我們的專案中,並在IDE中打開該檔。 然後,我們可以使用以下代碼實現基本的規則/驗證實施框架:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

有關上述代碼的一些說明:

- Dinner 類以"部分"關鍵字為開頭 - 這意味著其中包含的代碼將與 LINQ 生成/維護的類組合到 SQL 設計器並編譯為單個類。
- RuleRuleRule 類是一個説明類,我們將添加到專案中,允許我們提供有關規則違反的更多詳細資訊。
- 晚餐.GetRule違反()方法會導致評估我們的驗證和業務規則(我們將很快實施它們)。 然後,它返回一系列規則衝突物件,這些物件提供有關任何規則錯誤的更多詳細資訊。
- Dinner.IsValid 屬性提供了一個方便的幫助程式屬性,用於指示 Dinner 物件是否具有任何活動的規則衝突。 開發人員可以隨時使用 Dinner 物件主動檢查它(並且不會引發異常)。
- Dinner.OnValidate() 部分方法是 LINQ 到 SQL 提供的一個掛鉤,它允許我們在即將在資料庫中持久化 Dinner 物件的任何時間收到通知。 上述 OnValidate() 實現可確保在保存之前沒有規則違反規則。 如果處於無效狀態,它將引發異常,這將導致 LINQ 到 SQL 中止事務。

此方法提供了一個簡單的框架,我們可以將驗證和業務規則集成到其中。 現在,讓我們將以下規則添加到我們的 GetRule 違反() 方法:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

我們使用 C# 的「收益回報」功能來返回任何規則違反規則的序列。 上面的前六個規則檢查只是強制說,我們 Dinner 上的字串屬性不能為空或為空。 最後一條規則更有趣一點,並調用 PhoneValidator.IsValidNumber() 説明器方法,我們可以添加到我們的專案中,以驗證 ContactPhone 號碼格式是否與 Dinner 的國家/ 地區匹配。

我們可以使用 。NET 的正則表達式支持實現此電話驗證支援。 下面是一個簡單的電話驗證器實現,我們可以添加到我們的專案,使我們能夠添加特定於國家/地區的 Regex 模式檢查:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>處理驗證與業務邏輯衝突

現在,我們已經添加了上述驗證和業務規則代碼,每當我們嘗試創建或更新 Dinner 時,都將評估和強制執行驗證邏輯規則。

開發人員可以編寫如下代碼,以主動確定 Dinner 物件是否有效,並檢索其中所有衝突的清單,而不會引發任何異常:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

如果我們嘗試將 Dinner 保存為無效狀態,則當我們在 Dinner 儲存庫上調用 Save() 方法時,將引發異常。 這是因為 LINQ 到 SQL 在保存晚餐更改之前自動調用我們的 Dinner.OnValidate() 部分方法,並且我們在晚餐中添加了代碼。OnValidate() 如果晚餐中存在任何違反規則的行為,則引發異常。 我們可以捕獲此異常並被動檢索要修復的違規清單:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

由於驗證和業務規則在我們的模型層中實現,而不是 UI 層內,因此它們將在應用程式中的所有方案中應用和使用。 我們以後可以更改或添加業務規則,並讓所有與我們的 Dinner 物件一起使用的代碼都遵守它們。

在一個位置靈活地更改業務規則,而不使這些更改波及整個應用程式和 UI 邏輯,是編寫良好的應用程式的標誌,也是 MVC 框架有助於鼓勵的好處。

### <a name="next-step"></a>後續步驟

現在,我們有一個模型,我們可以用於查詢和更新我們的資料庫。

現在,讓我們向專案添加一些控制器和視圖,可用於構建圍繞它的 HTML UI 體驗。

> [!div class="step-by-step"]
> [前一個](create-a-database.md)
> [下一個](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
