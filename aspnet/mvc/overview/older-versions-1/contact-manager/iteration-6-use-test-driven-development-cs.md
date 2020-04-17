---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 反覆運算#6 = 使用測試驅動開發 (C#) |微軟文件
author: rick-anderson
description: 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: d0e8f30a075cc79c7410ffe1b8bf02da2bd44443
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542322"
---
# <a name="iteration-6--use-test-driven-development-c"></a>反覆項目 #6 – 使用測試導向的開發 (C#)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,我們添加聯繫人組。

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>編譯聯絡人管理ASP.NET MVC 應用程式 (C#)

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

在 Contact Manager 應用程式的上一次反覆運算中,我們創建了單元測試,為我們的代碼提供一個安全網。 創建單元測試的動機是使我們的代碼對更改更具彈性。 通過單元測試,我們可以愉快地對我們的代碼進行任何更改,並立即知道我們是否破壞了現有功能。

在此反覆運算中,我們將單元測試用於完全不同的目的。 在此反覆運算中,我們將單元測試用作稱為*測試驅動開發*的應用程式設計理念的一部分。 練習測試驅動開發時,首先編寫測試,然後針對測試編寫代碼。

更確切地說,在練習測試驅動開發時,在創建代碼時完成三個步驟(紅色/綠色/重構):

1. 編寫失敗的單元測試(紅色)
2. 編寫通過單元測試的代碼(綠色)
3. 重構代碼(重構)

首先,編寫單元測試。 單元測試應表達您希望代碼如何的行為的意圖。 首次創建單元測試時,單元測試應失敗。 測試應失敗,因為您尚未編寫滿足測試的任何應用程式代碼。

接下來,您只編寫足夠的代碼,以便單元測試通過。 目標是以最懶、最懶、最快的方式編寫代碼。 不應浪費時間考慮應用程式的體系結構。 相反,您應該專注於編寫滿足單元測試表達的意圖所需的最小代碼量。

最後,在編寫了足夠的代碼后,您可以退後一步考慮應用程式的整體體系結構。 在此步驟中,您利用軟體設計模式(如儲存庫模式)重寫(重構)代碼,以便代碼更可維護。 您可以在此步驟中無所畏懼地重寫代碼,因為單元測試涵蓋了您的代碼。

實踐測試驅動開發會帶來許多好處。 首先,測試驅動的開發迫使您專注於實際需要編寫的代碼。 由於您始終專注於編寫足夠的代碼以通過特定的測試,因此您無法遊蕩到雜草中,並編寫大量永遠不會使用的代碼。

其次,「測試第一」設計方法迫使您從如何使用代碼的角度編寫代碼。 換句話說,在練習測試驅動開發時,您會不斷從使用者的角度編寫測試。 因此,測試驅動的開發可以產生更清潔、更易懂的 API。

最後,測試驅動的開發迫使您編寫單元測試,作為編寫應用程式的正常過程的一部分。 隨著專案截止時間的臨近,測試通常是視窗外的第一件事。 另一方面,在實踐測試驅動開發時,您更有可能對編寫單元測試具有道德性,因為測試驅動開發使單元測試成為構建應用程式過程的核心。

> [!NOTE] 
> 
> 要瞭解有關測試驅動開發的更多內容,我建議您閱讀 Michael Feathers 的書,**以有效使用舊代碼**。

在此反覆運算中,我們將向聯繫人管理器應用程式添加新功能。 我們添加對聯繫人組的支援。 您可以使用"連絡人組"將聯絡人組織到"業務"和"朋友"組等類別中。

我們將遵循測試驅動開發過程,將這項新功能添加到我們的應用程式中。 我們將首先編寫單元測試,並針對這些測試編寫所有代碼。

## <a name="what-gets-tested"></a>測試內容

正如我們在上一次反覆運算中討論的那樣,您通常不會為數據訪問邏輯或視圖邏輯編寫單元測試。 您不會為資料訪問邏輯編寫單元測試,因為訪問資料庫的操作相對較慢。 您不為檢視邏輯編寫單元測試,因為造訪檢視需要旋轉 Web 伺服器,這是一個相對較慢的操作。 除非測試可以快速一遍又一遍地執行,否則不應編寫單元測試

由於測試驅動開發由單元測試驅動,所以我們最初側重於編寫控制器和業務邏輯。 我們避免觸摸資料庫或視圖。 在本教程結束之前,我們不會修改資料庫或創建視圖。 我們從可以測試的內容開始。

## <a name="creating-user-stories"></a>建立使用者情景

練習測試驅動開發時,您總是從編寫測試開始。 這立即提出了一個問題:你如何決定先寫什麼測試? 要回答這個問題,你應該編寫一組[**使用者情景**](http://en.wikipedia.org/wiki/User_stories)。

使用者情景是軟體要求的非常簡短(通常是一個句子)描述。 它應該是從使用者的角度編寫的對需求的非技術描述。

以下是描述新的聯絡人群組功能所需的功能的使用者情景集:

1. 使用者可以查看連絡人組的清單。
2. 用戶可以創建新的連絡人組。
3. 用戶可以刪除現有的連絡人組。
4. 創建新連絡人時,用戶可以選擇連絡人組。
5. 用戶可以在編輯現有聯繫人時選擇連絡人組。
6. 連絡人組清單顯示在「索引」檢視中。
7. 當用戶按一下連絡人組時,將顯示匹配連絡人的清單。

請注意,客戶完全可以理解此使用者情景清單。 沒有提到技術實施細節。

在構建應用程式的過程中,使用者情景集可能會變得更加精細。 您可以將使用者情景分解為多個情景(要求)。 例如,您可能決定創建新的聯繫人組應涉及驗證。 提交沒有名稱的聯繫人組應返回驗證錯誤。

創建使用者情景清單后,即可編寫第一個單元測試。 我們將首先創建用於查看聯繫人組列表的單位測試。

## <a name="listing-contact-groups"></a>列出聯絡人群組

我們的第一個使用者故事是,用戶應該能夠查看聯繫人組的清單。 我們需要用測試來表達這個故事。

通過右鍵單擊 ContactManager.測試專案中的控制器資料夾、選擇 **「添加、新建測試**」並選擇單元測試範本來創建新**的單元測試**(參見圖 1)。 GroupControllerTest.cs為新單元測試命名,然後單擊 **「確定**」按鈕。

[![新增組控制器測試單元測試](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**圖 01**: 新增群組控制器測試單元測試([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image2.png))

我們的第一個單元測試包含在清單 1 中。 此測試驗證組控制器的 Index() 方法是否傳回一組群組。 測試驗證在檢視數據中返回組的集合。

**清單 1 - 控制器\組控制器測試.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

當您首次在 Visual Studio 中鍵入清單 1 中的代碼時,您將獲得大量紅色波浪線。 我們尚未創建組控制器或組類。

此時,我們甚至不能構建應用程式,因此無法執行第一個單元測試。 很好 這算作一個失敗的測試。 因此,我們現在有權開始編寫應用程式代碼。 我們需要編寫足夠的代碼來執行我們的測試。

清單 2 中的組控制器類包含通過單元測試所需的最小代碼。 Index() 操作傳回靜態編碼的群組清單(組類在清單 3 中定義)。

**清單2 - 控制器\組控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**清單3 - 模型_組.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

將 GroupController 和組類添加到專案中後,我們的第一個單元測試將成功完成(參見圖 2)。 我們已經做了通過考試所需的最低工作。 是時候慶祝了。

[![成功!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**圖02:** 成功!([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>建立聯絡人群組

現在,我們可以轉到第二個使用者情景。 我們需要能夠創建新的聯繫組。 我們需要用測試來表達這個意圖。

清單4中的測試驗證,使用新組調用 Create() 方法會將組添加到 Index() 方法傳回的組清單中。 換句話說,如果我創建了一個新組,那麼我應該能夠從 Index() 方法返回的組列表中恢復新組。

**清單4 - 控制器\組控制器測試.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

清單4中的測試使用新的聯繫人組調用組控制器 Create() 方法。 接下來,測試驗證調用組控制器 Index() 方法返回檢視中的新組數據。

清單 5 中修改後的組控制器包含透過新測試所需的最小變更。

**清單5 - 控制器\組控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>清單 5 中的組控制器具有新的 Create() 操作。 此操作將組添加到組的集合中。 請注意,已修改 Index() 操作以返回組集合的內容。

再次,我們執行了通過單元測試所需的最低工作量。 對組控制器進行這些更改后,所有單元測試都通過。

## <a name="adding-validation"></a>新增驗證

在使用者情景中未明確說明此要求。 但是,要求集團有名稱是合理的。 否則,將聯繫人組織到組中將不是很有用。

清單6包含表示此意圖的新測試。 此測試驗證嘗試創建組而不提供名稱會導致模型狀態的驗證錯誤消息。

**清單6 - 控制器\組控制器測試.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

為了滿足此測試,我們需要向組類添加 Name 屬性(請參閱清單 7)。 此外,我們需要向組控制器的 Create() 操作添加一點驗證邏輯(參見清單 8)。

**清單7 - 模型_組.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**清單8 - 控制器\組控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

請注意,組控制器 Create() 操作現在同時包含驗證和資料庫邏輯。 目前,組控制器使用的資料庫僅包含記憶體中的集合。

## <a name="time-to-refactor"></a>重構時間

紅色/綠色/重構的第三步是重構部分。 此時,我們需要從代碼中退後一步,考慮如何重構應用程式以改進其設計。 重構階段是我們認真思考實現軟體設計原則和模式的最佳方式的階段。

我們可以自由地修改我們的代碼,我們選擇以任何方式改進代碼的設計。 我們有一個單元測試安全網,以防止我們破壞現有功能。

現在,從良好的軟體設計來看,我們的集團控制器是一團糟。 組控制器包含一堆的驗證和數據訪問代碼。 為了避免違反單一責任原則,我們需要將這些關注分為不同的類別。

我們的重構組控制器類包含在清單 9 中。 控制器已修改為使用 ContactManager 服務層。 這與我們與聯繫人控制器一起使用的服務層相同。

清單10包含添加到 ContactManager 服務層以支援驗證、列出和創建組的新方法。 IContactManager 服務介面已更新,以包括新方法。

清單11包含一個新的FakeContactManagerManager儲存庫類,該類實現了IContactManagerRepository介面。 與同時實現 IContactManager Repository 介面的實體聯繫人管理器儲存庫類不同,我們新的 FakeContactManagerManager Repository 類不與資料庫通信。 FakeContactManagerManagerRepository 類使用記憶體中集合作為資料庫的代理。 我們將在單元測試中將此類用作假存儲庫層。

**清單 9 - 控制器\組控制器.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**清單 10 - 控制器\連絡管理員服務.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**清單11 - 控制器\假連絡人管理員儲存庫.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

修改 IContactManager 儲存庫介面需要用於在實體連絡人管理員儲存庫類別中實現 CreateGroup() 和清單組()方法。 最懶惰和最快的方法是添加如下所示的存根方法:   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

最後,對應用程式設計的這些更改要求我們對單元測試進行一些修改。 現在,在執行單元測試時,我們需要使用假聯繫人管理器存儲庫。 更新後的 GroupControllerTest 類包含在清單 12 中。

**清單12 - 控制器\組控制器測試.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

在我們進行所有這些更改后,我們再次通過所有單元測試。 我們已經完成了整個紅色/綠色/重構週期。 我們已經實現了前兩個使用者情景。 現在,我們支持使用者情景中表達的要求單元測試。 實現其餘使用者情景涉及重複相同的紅色/綠色/重構週期。

## <a name="modifying-our-database"></a>變更資料庫

不幸的是,儘管我們滿足了單元測試表達的所有要求,但我們的工作並沒有完成。 我們仍然需要修改我們的資料庫。

我們需要創建新的組資料庫表。 請遵循下列步驟：

1. 在「伺服器資源管理器」視窗中,右鍵按一下「表」資料夾並選擇功能表選項 **「添加新表**」。
2. 輸入下表設計器中描述的兩列。
3. 將 Id 列標記為主鍵和標識列。
4. 按下軟碟的圖示,保存具有名稱組的新錶。

<a id="0.11_table01"></a>

| **資料行名稱** | **資料類型** | **允許 Null** |
| --- | --- | --- |
| Id | int | False |
| 名稱 | nvarchar(50) | False |

接下來,我們需要從"連絡人"表中刪除所有資料(否則,我們將無法在"連絡人"和"組"表之間創建關係)。 請遵循下列步驟：

1. 右鍵按兩下"連絡人"表並選擇功能表選項 **"顯示表數據**"。
2. 刪除所有行。

接下來,我們需要定義組資料庫表和現有聯繫人資料庫表之間的關係。 請遵循下列步驟：

1. 按兩下伺服器資源管理器視窗中的"連絡人"表以打開表設計器。
2. 向名為 GroupId 的"連絡人"表添加新整數列。
3. 按下「關係」按鈕以打開「外鍵關係」對話框(參見圖 3)。
4. 按一下 [新增] 按鈕。
5. 按下「表和列規範」按鈕旁邊的省略號按鈕。
6. 在"表和列"對話框中,選擇組作為主鍵表,選擇 Id 作為主鍵列。 選擇"連絡人"作為外鍵表,將 GroupId 作為外鍵列(參見圖 4)。 按一下 [確定] 按鈕。
7. 在 **'插入"和"更新規範"** 下,選擇**刪除規則**的值 **「級聯**」。。
8. 按下「關閉」按鈕以關閉「外鍵關係」對話方塊。
9. 按下「儲存」按鈕將更改儲存到"連絡人"表。

[![建立資料庫表關係](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**圖 03**: 建立資料庫表關係([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image6.png))

[![指定表關係](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**圖 04**:指定表格([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image8.png))

### <a name="updating-our-data-model"></a>更新資料模型

接下來,我們需要更新數據模型以表示新的資料庫表。 請遵循下列步驟：

1. 按兩下「模型」資料夾中的 ContactManagerModel.edmx 檔以打開實體設計器。
2. 右鍵按一下「設計器」曲面,然後從資料庫中選擇功能表選項 **「更新模型**」。
3. 在"更新嚮導"中,選擇"組"表並按兩下"完成"按鈕(參見圖 5)。
4. 右鍵按一下「組實體」並選擇功能表選項 **「重新命名**」。 將*組*實體的名稱更改為*組*(單數)。
5. 右鍵按一下顯示在「聯繫人」實體底部的「組導航屬性」。 將*組*導航屬性的名稱更改為*組*(單數)。

[![從資料庫更新實體框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**圖 05**:從資料庫更新實體框架模型([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image10.png))

完成這些步驟后,數據模型將同時表示"聯繫人"和"組"表。 實體設計器應顯示兩個實體(參見圖 6)。

[![實體設計器顯示群組與聯絡人](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**圖 06**: 實體設計器顯示群組與聯絡人([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image12.png))

### <a name="creating-our-repository-classes"></a>建立我們的儲存庫類別

接下來,我們需要實現我們的存儲庫類。 在此反覆運算過程中,我們在編寫代碼以滿足單元測試的同時,向IContactManagerRepository介面添加了幾種新方法。 IContactManager儲存庫介面的最終版本包含在清單14中。

**清單14 - 型號\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

我們實際上尚未實現與使用聯繫人組相關的任何方法。 目前,實體聯繫人管理體儲存庫類具有IContactManagerRepository介面中列出的每個連絡人組方法的存根方法。 例如,ListGroups() 方法目前如下所示:

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

存根方法使我們能夠編譯應用程式並通過單元測試。 但是,現在是時候實際實現這些方法了。 實體聯繫人管理器儲存庫類的最終版本包含在清單 13 中。

**清單13 - 模型_實體連絡人管理員儲存庫.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>建立檢視

使用預設ASP.NET檢視引擎時,ASP.NET MVC 應用程式。 因此,您不會創建檢視以回應特定的單元測試。 但是,由於沒有檢視的應用程式將毫無用處,因此,如果不創建和修改 Contact Manager 應用程式中的視圖,我們就無法完成此反覆運算。

我們需要建立以下用於管理連絡人組的新檢視(參見圖 7):

- 檢視_組\索引.aspx - 顯示聯絡人群組清單
- 檢視\組\刪除.aspx - 顯示用於刪除聯絡人群組的確認表單

[![群組索引檢視](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**圖 07**: 群組索引檢視([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image14.png))

我們需要修改以下現有檢視,以便它們包括聯絡人組:

- 檢視\Home_Create.aspx
- 檢視\首頁\編輯.aspx
- 檢視\首頁\索引.aspx

通過查看本教程附帶的 Visual Studio 應用程式,可以查看修改後的檢視。 例如,圖 8 說明瞭聯繫人索引視圖。

[![連絡人索引檢視](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**圖 08**: 連絡人索引檢視([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-cs/_static/image16.png))

## <a name="summary"></a>總結

在此反覆運算中,我們遵循測試驅動的開發應用程式設計方法,向 Contact Manager 應用程式添加了新功能。 我們首先創建一組使用者情景。 我們創建了一組單元測試,這些測試對應於使用者情景表達的要求。 最後,我們編寫的代碼足夠滿足單元測試表達的要求。

完成編寫足夠的代碼以滿足單元測試表達的要求后,我們更新了資料庫和視圖。 我們將新的組表添加到我們的資料庫中,並更新了實體框架數據模型。 我們還創建並修改了一組視圖。

在下一次反覆運算(最後反覆運算)中,我們重寫應用程式以利用Ajax。 通過使用Ajax,我們將提高聯繫人管理器應用程式的回應性和性能。

> [!div class="step-by-step"]
> [前一個](iteration-5-create-unit-tests-cs.md)
> [下一個](iteration-7-add-ajax-functionality-cs.md)
