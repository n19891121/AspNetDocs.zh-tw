---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 反覆運算#4 = 使應用程式鬆散耦合 (C#) |微軟文件
author: rick-anderson
description: 在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。 如需...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: c4ba6c9a130995c095653f4316a5fefdfc03b91d
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542361"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>反覆項目 #4 – 讓應用程式鬆散耦合 (C#)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。 例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。

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

在 Contact Manager 應用程式的第四個反覆運算中,我們重構應用程式以使應用程式更鬆散耦合。 當應用程式鬆散耦合時,可以在應用程式一個部分修改代碼,而無需修改應用程式其他部分中的代碼。 鬆散耦合的應用程式對更改更具彈性。

目前,Contact Manager 應用程式使用的所有數據訪問和驗證邏輯都包含在控制器類中。 這是個壞主意。 每當需要修改應用程式的一個部分時,您都有可能將 Bug 引入應用程式的另一部分。 例如,如果修改驗證邏輯,則有在數據訪問或控制器邏輯中引入新 Bug 的風險。

> [!NOTE] 
> 
> (SRP),類不應有超過一個更改的原因。 混合控制器、驗證和資料庫邏輯嚴重違反了單一責任原則。

可能需要修改應用程式的原因有多種。 您可能需要向應用程式添加新功能,可能需要修復應用程式中的 Bug,或者可能需要修改應用程式的實現方式。 應用程式很少是靜態的。 它們往往隨著時間的推移而生長和變異。

例如,假設您決定更改實現數據訪問層的方式。 現在,連絡人管理器應用程式使用Microsoft實體框架存取資料庫。 但是,您可能決定遷移到新的或替代的數據訪問技術,如ADO.NET數據服務或 NHibernate。 但是,由於數據訪問代碼不與驗證和控制器代碼隔離,因此如果不修改與數據訪問沒有直接關係的其他代碼,就無法修改應用程式中的數據訪問代碼。

另一方面,當應用程式耦合鬆散時,您可以對應用程式的一個部分進行更改,而無需接觸應用程式的其他部分。 例如,無需修改驗證或控制器邏輯即可切換數據訪問技術。

在此反覆運算中,我們利用了多種軟體設計模式,使我們能夠將我們的 Contact Manager 應用程式重構為更鬆散耦合的應用程式。 完成後,聯繫人管理器不會執行以前未執行的任何操作。 但是,我們將來能夠更輕鬆地更改應用程式。

> [!NOTE] 
> 
> 重構是重寫應用程式的過程,這樣它不會丟失任何現有功能。

## <a name="using-the-repository-software-design-pattern"></a>使用儲存函式庫軟體設計模式

我們的第一個變化是利用稱為存儲庫模式的軟體設計模式。 我們將使用儲存庫模式將數據訪問代碼與應用程式的其餘部分隔離開來。

實現儲存庫模式需要我們完成以下兩個步驟:

1. 建立介面
2. 建立式介面的具體類別

首先,我們需要創建一個介面來描述我們需要執行的所有數據訪問方法。 IContactManager儲存庫介面包含在清單1中。 此介面描述了五種方法:創建連絡人、刪除連絡人、編輯連絡人、獲取聯繫人和清單聯繫人()。

**清單 1 - 型號\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

接下來,我們需要創建一個實現 IContactManager Repository 介面的具體類。 由於我們使用 Microsoft 實體框架訪問資料庫,因此我們將創建一個名為實體聯繫人管理器儲存庫的新類。 此類包含在清單 2 中。

**清單2 - 模型_實體連絡人管理員儲存庫.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

請注意,實體聯繫人管理體儲存庫類實現了IContactManager儲存庫介面。 類實現該介面描述的所有五種方法。

您可能想知道為什麼我們需要處理一個介面。 為什麼我們需要同時創建介面和實現它的類?

除了一個例外,我們應用程式的其餘部分將與介面而不是具體類進行交互。 我們將調用 IContactManagerRepository 介面公開的方法,而不是調用實體ContactManagerRepository類公開的方法。

這樣,我們可以使用新類實現介面,而無需修改應用程式的其餘部分。 例如,在未來某個日期,我們可能想要實現實現 IContactManagerRepository 介面的數據服務聯繫人管理器儲存庫類。 DataServicesContactManagerManagerRepository 類可能使用ADO.NET數據服務來訪問資料庫而不是Microsoft實體架構。

如果我們的應用程式代碼是根據 IContactManagerRepository 介面而不是具體的 EntityContactManagerManager Repository 類程式設計的,那麼我們可以切換具體類,而無需修改我們代碼的任何其餘部分。 例如,我們可以從實體聯繫人管理體儲存庫類切換到 DataServicesContactManagerManagerRepository 類,而無需修改我們的數據訪問或驗證邏輯。

針對介面(抽象)而不是具體類進行程式設計使我們的應用程式更具彈性,從而對更改進行程式設計。

> [!NOTE] 
> 
> 您可以通過選擇功能表選項「重構」,提取介面,從 Visual Studio 中的特定類快速創建介面。 例如,您可以先創建實體聯繫人管理體儲存庫類,然後使用提取介面自動生成 IContactManagerRepository 介面。

## <a name="using-the-dependency-injection-software-design-pattern"></a>使用相依項性設計模式

現在,我們已經將數據訪問代碼遷移到單獨的存儲庫類,我們需要修改我們的聯繫人控制器才能使用此類。 我們將利用稱為依賴注入的軟體設計模式,在我們的控制器中使用存儲庫類。

修改後的連絡人控制器包含在清單3中。

**清單3 - 控制器\聯絡控制器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

請注意,清單 3 中的聯繫人控制器有兩個構造函數。 第一個構造函數將IContactManagerRepository 介面的具體實例傳遞給第二個構造函數。 聯絡人控制器類別使用*建構函式相依項 。*

使用實體聯繫人管理體儲存庫類的唯一位置位於第一個構造函數中。 類的其餘部分使用IContactManagerRepository介面,而不是具體的實體聯繫人管理體儲存庫類。

這樣,將來可以輕鬆切換 IContactManagerRepository 類的實現。 如果要使用 DataServicesContact 儲存庫類而不是實體聯繫人管理體儲存庫類,只需修改第一個構造函數。

建構函數依賴項注入也使聯繫人控制器類非常可測試。 在單元測試中,您可以通過透過 IContactManagerRepository 類的模擬實現來實例化連絡人控制器。 在下一次反覆運算中,當我們為聯繫人管理器應用程式構建單元測試時,依賴項注入的此功能對我們非常重要。

> [!NOTE] 
> 
> 如果要將 Contact 控制器類與 IContactManagerRepository 介面的特定實現完全分離,則可以利用支援依賴項注入的框架,如結構映射或 Microsoft 實體框架 (MEF)。 使用依賴項注入框架,您無需在代碼中引用具體類。

## <a name="creating-a-service-layer"></a>建立服務層

您可能已經注意到,我們的驗證邏輯仍然與清單 3 中修改後的控制器類中的控制器邏輯混合在一起。 出於隔離數據訪問邏輯的一個個好主意,最好隔離我們的驗證邏輯。

為了解決此問題,我們可以創建一個單獨的[*服務層*](http://martinfowler.com/eaaCatalog/serviceLayer.html)。 服務層是一個單獨的層,我們可以插入控制器和存儲庫類之間。 服務層包含我們的業務邏輯,包括我們所有的驗證邏輯。

聯繫人管理員服務包含在清單 4 中。 它包含來自聯繫人控制器類的驗證邏輯。

**清單4 - 型號_聯繫管理員服務.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

請注意,聯繫人管理器服務的構造函數需要驗證字典。 服務層通過此驗證字典與控制器層通信。 在討論修飾器模式時,我們將在下一節中詳細討論驗證詞典。

此外,請注意,聯繫人管理器服務實現了IContactManager服務介面。 您應該始終努力針對介面而不是具體類進行程式設計。 連絡人管理員應用程式中的其他類不直接與聯繫人管理器服務類交互。 相反,除了一個例外,聯繫人管理器應用程式的其餘部分根據IContactManager服務介面進行程式設計。

IContactManager 服務介面包含在清單 5 中。

**清單5 - 型號_IContactManager服務.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

修改後的聯繫人控制器類包含在清單 6 中。 請注意,連絡人控制器不再與聯繫人管理體儲存庫進行交互。 相反,連絡人控制器與聯繫人管理員服務進行互動。 每個圖層都盡可能與其他圖層隔離。

**清單 6 - 控制器\聯絡控制器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

我們的應用程式不再違反單一責任原則 (SRP)。 清單6中的聯繫人控制器除控制應用程式執行流外,已被剝奪了所有責任。 所有驗證邏輯都已從"連絡人"控制器中刪除,並推送到服務層。 所有資料庫邏輯都已推送到存儲庫層。

## <a name="using-the-decorator-pattern"></a>使用修飾器模式

我們希望能夠將服務層與控制器層完全分離。 原則上,我們應該能夠在與控制器層分開的程式集中編譯我們的服務層,而無需添加對 MVC 應用程式的引用。

但是,我們的服務層需要能夠將驗證錯誤消息傳遞回控制器層。 我們如何使服務層在不耦合控制器和服務層的情況下通信驗證錯誤消息? 我們可以利用軟體設計模式,稱為[裝飾模式](http://en.wikipedia.org/wiki/Decorator_pattern)。

控制器使用名為 ModelState 的 ModelState 字典來表示驗證錯誤。 因此,您可能受誘惑將 ModelState 從控制器層傳遞到服務層。 但是,在服務層中使用 ModelState 將使服務層依賴於ASP.NET MVC 框架的功能。 這將很糟糕,因為有一天,您可能希望將服務層與 WPF 應用程式一起使用,而不是使用ASP.NET MVC 應用程式。 在這種情況下,您不希望引用ASP.NET MVC 框架來使用 ModelState字典類。

修飾器模式使您能夠在新類中包裝現有類,以實現介面。 我們的聯繫人管理器專案包括清單 7 中包含的 ModelStateWrapper 類。 ModelStateWrapper 類實現清單 8 中的介面。

**清單7 - 模型_驗證_模型狀態包裝器.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**清單8 - 模型_驗證_驗證字典.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

如果您仔細查看清單 5,您將看到 ContactManager 服務層專用 IValidationa 字典介面。 連絡人管理器服務不依賴於 ModelState 字典類。 當聯絡人控制器建立 ContactManager 服務時,控制器將像這樣包裝其 ModelState:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>總結

在此反覆運算中,我們沒有向聯繫人管理器應用程式添加任何新功能。 此反覆運算的目標是重構聯繫人管理器應用程式,以便更易於維護和修改。

首先,我們實現了存儲庫軟體設計模式。 我們將所有數據訪問代碼遷移到單獨的 ContactManager 儲存庫類。

我們還將驗證邏輯與控制器邏輯隔離開來。 我們創建了一個單獨的服務層,其中包含我們所有的驗證代碼。 控制器層與服務層交互,服務層與存儲庫層交互。

創建服務層時,我們利用修飾器模式將 ModelState 與服務層隔離開來。 在我們的服務層中,我們根據 I 驗證詞典介面而不是 ModelState 進行了程式設計。

最後,我們利用了名為依賴項注入模式的軟體設計模式。 此模式使我們能夠針對介面(抽象)而不是具體類進行程式設計。 實現依賴項注入設計模式也使我們的代碼更具可測試性。 在下一個反覆運算中,我們將單元測試添加到專案中。

> [!div class="step-by-step"]
> [前一個](iteration-3-add-form-validation-cs.md)
> [下一個](iteration-5-create-unit-tests-cs.md)
