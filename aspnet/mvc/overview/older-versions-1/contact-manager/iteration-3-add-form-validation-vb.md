---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 反覆運算#3 = 新增表單驗證 (VB) |微軟文件
author: rick-anderson
description: 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證了 emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ee2f40996873a7af2eaa255edd5f157c3fefb29
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542387"
---
# <a name="iteration-3--add-form-validation-vb"></a>反覆項目 #3 – 新增表單驗證 (VB)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證電子郵件地址和電話號碼。

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

在聯繫人管理器應用程式的第二次反覆運算中,我們添加基本表單驗證。 我們防止人員提交聯繫人而不輸入所需表單欄位的值。 我們還驗證電話號碼和電子郵寄地址(參見圖 1)。

[![[New Project] \(新增專案\) 對話方塊](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**圖 01**: 具有認證的表單([按下以檢視全尺寸影像](iteration-3-add-form-validation-vb/_static/image2.png))

在此反覆運算中,我們將驗證邏輯直接添加到控制器操作中。 通常,這不是向ASP.NET MVC 應用程式添加驗證的建議方法。 更好的方法是將應用程序的驗證邏輯放在單獨的[服務層](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。 在下一次反覆運算中,我們將重構聯繫人管理器應用程式,以使應用程式更具可維護性。

在此反覆運算中,為了簡單化,我們手動編寫所有驗證代碼。 我們可以利用驗證框架,而不是自己編寫驗證代碼。 例如,可以使用 Microsoft 企業庫驗證應用程式區 (VAB) 來實現 ASP.NET MVC 應用程式的驗證邏輯。 要瞭解有關驗證應用程式塊的更多,請參閱:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>將驗證新增到建立檢視

讓我們首先向"創建"視圖添加驗證邏輯。 幸運的是,由於我們使用 Visual Studio 生成了"創建"視圖,因此"創建"視圖已包含顯示驗證消息所需的所有使用者介面邏輯。 "創建"檢視包含在清單 1 中。

**清單 1 - [檢視]連絡人\創建.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

欄位驗證錯誤類用於設定 Html.驗證 Message() 説明程式呈現的輸出的樣式。 輸入驗證錯誤類用於設定 Html.TextBox() 説明程式呈現的文字框(輸入)的樣式。 驗證摘要錯誤類用於設置 Html.驗證摘要() 説明程式呈現的無序列表的樣式。

> [!NOTE] 
> 
> 您可以修改本節中描述的樣式表類,以自定義驗證錯誤消息的外觀。

## <a name="adding-validation-logic-to-the-create-action"></a>將驗證邏輯加入到建立作業

現在,"創建"視圖從不顯示驗證錯誤消息,因為我們尚未編寫邏輯來生成任何消息。 為了顯示驗證錯誤消息,您需要將錯誤消息添加到 ModelState。

> [!NOTE] 
> 
> 當將表單欄位的值分配給屬性時,UpdateModel() 方法會自動將錯誤消息添加到 ModelState。 例如,如果您嘗試將字串「apple」分配給接受 DateTime 值的 DateDate 屬性,則 UpdateModel() 方法將錯誤添加到 ModelState。

清單 2 中修改的 Create() 方法包含一個新部分,用於在新聯繫人插入資料庫之前驗證 Contact 類的屬性。

**清單2 - 控制器\聯絡控制器.vb(透過認證建立)**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

驗證部分強制執行四個不同的驗證規則:

- FirstName 屬性的長度必須大於零(它不能僅由空格組成)
- LastName 屬性的長度必須大於零(它不能僅由空格組成)
- 如果 Phone 屬性具有值(長度大於 0),則 Phone 屬性必須匹配正則運算式。
- 如果 Email 屬性的值(長度大於 0),則 Email 屬性必須與正則運算式匹配。

當存在驗證規則衝突時,在 AddModelError() 方法的説明下,將一條錯誤消息添加到 ModelState。 將消息添加到 ModelState 時,會提供屬性的名稱和驗證錯誤消息的文本。 此錯誤訊息由 Html.驗證摘要() 和 Html.驗證消息() 説明器方法顯示在檢視中。

執行驗證規則後,將檢查 ModelState 的「IsValid」屬性。 將任何驗證錯誤消息添加到 ModelState 時,「IsValid」屬性將返回 false。 如果驗證失敗,則使用錯誤消息重新顯示"創建"表單。

> [!NOTE] 
> 
> 我收到用於驗證從正則表達式存儲庫的電話號碼和電子郵寄地址的正則運算式,[*http://regexlib.com*](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>將驗證邏輯加入編輯操作

編輯() 操作更新連絡人。 Edit() 操作需要執行與 Create() 操作完全相同的驗證。 我們不應複製相同的驗證代碼,而應重構聯繫人控制器,以便 Create() 和 Edit() 操作調用相同的驗證方法。

修改後的聯繫人控制器類包含在清單 3 中。 此類具有在 Create() 和 Edit() 操作中調用的新驗證連絡人() 方法。

**清單3 - 控制器\聯絡控制器.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>總結

在此反覆運算中,我們將基本表單驗證添加到我們的聯繫人管理器應用程式中。 我們的驗證邏輯可防止使用者提交新連絡人或編輯現有連絡人,而不提供 Name 和 LASTName 屬性的值。 此外,用戶必須提供有效的電話號碼和電子郵寄地址。

在此反覆運算中,我們以最簡單的方式將驗證邏輯添加到我們的聯繫人管理器應用程式中。 但是,從長期來看,將驗證邏輯混合到控制器邏輯中將給我們帶來問題。 隨著時間的推移,我們的應用程式將更難維護和修改。

在下一次反覆運算中,我們將重構我們的驗證邏輯和資料庫存取邏輯的控制器。 我們將利用多種軟體設計原則,使我們能夠創建一個更鬆散耦合、更可維護的應用程式。

> [!div class="step-by-step"]
> [前一個](iteration-2-make-the-application-look-nice-vb.md)
> [下一個](iteration-4-make-the-application-loosely-coupled-vb.md)
