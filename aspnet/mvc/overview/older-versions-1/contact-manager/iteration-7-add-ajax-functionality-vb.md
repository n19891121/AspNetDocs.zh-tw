---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: 反覆運算#7 = 添加 Ajax 功能 (VB) |微軟文件
author: rick-anderson
description: 在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: 04eaaa129a56b765c090e64118ed528c65987b50
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542296"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>反覆項目 #7 – 新增 Ajax 功能 (VB)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。

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

在此反覆運算的聯繫人管理器應用程式中,我們將重構應用程式以使用 Ajax。 通過使用Ajax,我們使我們的應用程式回應更快。 當只需要更新頁面中的某個區域時,我們可以避免呈現整個頁面。

我們將重構索引視圖,以便每當有人選擇新的聯繫人組時,我們就不需要重新顯示整個頁面。 相反,當有人單擊聯繫人組時,我們只會更新聯繫人清單,並單獨保留頁面的其餘部分。

我們還將更改刪除連結的工作方式。 我們將顯示 JAVAScript 確認對話框,而不是顯示單獨的確認頁。 如果確認要刪除連絡人,則對伺服器執行 HTTP DELETE 操作以從資料庫中刪除連絡人記錄。

此外,我們將利用 jQuery 將動畫效果添加到索引檢視中。 當從伺服器提取新的聯繫人清單時,我們將顯示一個動畫。

最後,我們將利用ASP.NETAJAX框架支援來管理瀏覽器歷史記錄。 每當執行 Ajax 調用以更新聯繫人清單時,我們都會創建歷史記錄點。 這樣,瀏覽器的後退和向前按鈕將工作。

## <a name="why-use-ajax"></a>為什麼要使用Ajax?

使用Ajax有很多好處。 首先,將Ajax功能添加到應用程式中可以提供更好的用戶體驗。 在正常 Web 應用程式中,每次使用者執行操作時,都必須將整個頁面發回伺服器。 每當執行操作時,瀏覽器都會鎖定,用戶必須等待,直到提取並重新顯示整個頁面。

在桌面應用程序的情況下,這是不可接受的體驗。 但是,傳統上,我們生活在一個Web應用程序的情況下,這種糟糕的用戶體驗,因為我們不知道我們可以做得更好。 我們認為這是Web應用程式的一個限制,而實際上,這隻是我們想像力的一個限制。

在 Ajax 應用程式中,無需僅更新頁面就停止用戶體驗。 相反,您可以在後台執行非同步請求以更新頁面。 在頁面部分更新時,不會強制使用者等待。

通過使用Ajax,您還可以提高應用程式的性能。 請考慮聯繫人管理器應用程式現在如何工作,而無需 Ajax 功能。 按一下聯絡人組時,必須重新顯示整個索引檢視。 必須從資料庫伺服器檢索聯繫人列表和連絡人組清單。 所有這些資料都必須通過從 Web 伺服器到 Web 瀏覽器的線傳遞。

但是,在將 Ajax 功能添加到應用程式後,我們可以避免在使用者單擊聯繫人組時重新播放整個頁面。 我們不再需要從資料庫獲取聯繫人組。 我們也不需要將整個索引視圖推送到導線上。 通過使用 Ajax,我們減少了資料庫伺服器必須執行的工作量,並減少了應用程式所需的網路流量。

## <a name="don-t-be-afraid-of-ajax"></a>不要害怕阿賈克斯

一些開發人員避免使用Ajax,因為他們擔心低級瀏覽器。 他們希望確保他們的 Web 應用程式在不受支援 JAvaScript 的瀏覽器訪問時仍然有效。 由於Ajax依賴於JAVAScript,一些開發人員避免使用Ajax。

但是,如果您對如何實現Ajax很小心,則可以構建同時使用高級瀏覽器和低級瀏覽器的應用程式。 我們的連絡人管理員應用程式將適用於支援 JAVAScript 的瀏覽器和不支援的瀏覽器。

如果將連絡人管理員應用程式與支援 JAvaScript 的瀏覽器一起使用,那麼您將有更好的用戶體驗。 例如,當您按一下連絡人組時,將僅更新顯示聯絡人的頁面區域。

另一方面,如果將聯繫人管理器應用程式用於不支援 JAVAScript(或禁用了 JAVAScript)的瀏覽器,則您的使用者體驗將稍遜一籌。 例如,當您按一下連絡人組時,必須將整個 Index 檢視發回瀏覽器才能顯示聯絡人的匹配清單。

## <a name="adding-the-required-javascript-files"></a>新增需要的 JavaScript 檔案

我們需要使用三個 JavaScript 檔將 Ajax 功能添加到我們的應用程式中。 所有這些檔都包含在新的ASP.NET MVC 應用程式的文本資料夾中。

如果您計劃在應用程式中的多個頁面中使用Ajax,那麼在應用程式的檢視母版頁中包含所需的 JAVAScript 檔是有意義的。 這樣,JavaScript 檔將自動包含在應用程式中的所有頁面中。

在檢視母版頁&lt;的頭部&gt;標記中加入以下 JAVAScript:

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>重構索引檢視以使用 Ajax

讓我們首先修改我們的 Index 檢視,以便單擊連絡人組僅更新顯示聯絡人的檢視區域。 圖 1 中的紅色框包含我們要更新的區域。

[![只更新聯絡人](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**圖 01**:僅更新聯絡人([按下以檢視全尺寸影像](iteration-7-add-ajax-functionality-vb/_static/image2.png))

第一步是將要異步更新的視圖部分分離為單獨的部分(視圖使用者控件)。 顯示聯絡人表的 Index 檢視部分已移動到清單 1 中的部分。

**清單 1 - 檢視\連絡人\連絡人清單.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

請注意,清單 1 中的部分具有與索引視圖不同的模型。 %@ Page&lt;&gt;%&lt;指令中的*繼承*屬性指定從 ViewUserControl 組&gt;類別的部分繼承。

更新的索引檢視包含在清單 2 中。

**清單2 - 檢視\連絡人\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

關於清單2中更新的視圖,您應該注意兩件事。 首先,請注意,移動到部分的所有內容都將替換為對 Html.Render 部分()的調用。 首次請求索引檢視以顯示初始連絡人集時調用 Html.Render 部分() 方法。

其次,請注意,用於顯示連絡人組的 Html.ActionLink() 已替換為 Ajax.ActionLink()。 Ajax.ActionLink()使用以下參數呼叫:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

第一個參數表示要顯示的連結的文本,第二個參數表示路由值,第三個參數表示 Ajax 選項。 在這種情況下,我們使用 UpdateTargetId Ajax 選項來指向要在&lt;&gt;Ajax 請求完成後更新的 HTML div 標記。 我們希望使用新的聯繫人清單&lt;&gt;更新 div 標記。

聯繫人控制器的更新索引() 方法包含在清單 3 中。

**清單3 - 控制器\連絡控制器.vb(索引方法)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

更新的 Index() 操作有條件地返回兩件事情之一。 如果 Ajax 請求調用了 Index() 操作,則控制器返回部分。 否則,Index() 操作將返回整個檢視。

請注意,當 Ajax 請求調用時,Index() 操作不需要返回盡可能多的數據。 在正常請求的上下文中,Index 操作返回所有連絡人組和所選連絡人組的清單。 在 Ajax 請求的上下文中,Index() 操作僅返回選定的組。 Ajax 意味著資料庫伺服器上的工作更少。

我們修改的 Index 檢視適用於上層瀏覽器和低級瀏覽器。 如果按一下連絡人組,並且您的瀏覽器支援 JAVAScript,則僅更新包含連絡人清單的檢視區域。 另一方面,如果您的瀏覽器不支援 JAvaScript,則整個檢視將更新。

我們更新的索引視圖有一個問題。 按一下連絡人組時,所選組不會突出顯示。 由於組清單顯示在 Ajax 請求期間更新的區域之外,因此不會突出顯示正確的組。 我們將在下一節中解決此問題。

## <a name="adding-jquery-animation-effects"></a>新增 jQuery 動畫效果

通常,當您單擊網頁中的連結時,可以使用瀏覽器進度欄來檢測瀏覽器是否主動獲取更新的內容。 另一方面,當執行 Ajax 請求時,瀏覽器進度列不顯示任何進度。 這會使用戶感到緊張。 您如何知道瀏覽器是否已凍結?

有幾種方法可以向使用者指示在執行 Ajax 請求時正在執行工作。 一種方法是顯示一個簡單的動畫。 例如,當 Ajax 請求開始並淡入該區域時,可以淡出該區域。"

我們將使用 Microsoft ASP.NET MVC 框架中包含的 jQuery 庫來創建動畫效果。 更新的索引檢視包含在清單 4 中。

**清單4 - 檢視_連絡人_Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

請注意,更新的索引檢視包含三個新的 JAVAScript 函數。 按一下新連絡人組時,前兩個函數使用 jQuery 淡入淡出並淡入聯繫人清單中。 當 Ajax 請求導致錯誤(例如,網路超時)時,第三個函數將顯示一條錯誤消息。

第一個函數還負責突出顯示所選組。 類* 選取的屬性將添加到單擊的元素的父元素(LI 元素)。 同樣,jQuery 便於選擇正確的元素並添加 CSS 類。

這些文本在Ajax.ActionLink())AjaxOptions參數的説明下與組連結相關聯。 更新的Ajax.ActionLink()方法呼叫以下所示:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>新增瀏覽器歷史記錄支援

通常,當您按下連結以更新頁面時,您的瀏覽器歷史記錄將更新。 這樣,您可以按一下瀏覽器"後退"按鈕以及時移回頁面的上一個狀態。 例如,如果您按兩下「好友聯繫人組」然後單擊「業務聯繫人組」,則可以按一下瀏覽器「後退」按鈕,在選擇「好友聯繫人組」時導航回頁面狀態。

遺憾的是,執行 Ajax 請求不會自動更新瀏覽器歷史記錄。 如果按一下聯絡人組,並且使用 Ajax 請求檢索匹配聯絡人的清單,則瀏覽器歷史記錄不會更新。 選擇新的連絡人組後,不能使用瀏覽器"後退"按鈕導航回連絡人組。

如果您希望使用者在執行 Ajax 請求後能夠使用瀏覽器" 後退「 按鈕,則需要執行更多工作」。 您需要利用ASP.NET AJAX 框架中建構的瀏覽器歷史記錄管理功能。

ASP.NET AJAX 瀏覽器歷史記錄,您需要執行以下三項操作:

1. 通過將啟用瀏覽器歷史記錄屬性設置為 true,啟用瀏覽器歷史記錄。
2. 通過調用 addHistoryPoint() 方法,在檢視狀態發生變化時保存歷史記錄點。
3. 引發導航事件時重建視圖的狀態。

更新的索引檢視包含在清單 5 中。

**清單5 - 檢視_連絡人_Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

在清單5中,瀏覽器歷史記錄在頁面 Init() 函數中啟用。 pageInit() 函數還用於設置導航事件的事件處理程式。 每當瀏覽器「前進」或「後退」按鈕導致頁面狀態更改時,將引發導航事件。

按一下連絡人組時將調用開始連絡人清單() 方法。 此方法通過調用 add 歷史點() 方法創建新的歷史記錄點。 按一下的連絡人組的 ID 將添加到歷史記錄中。

從連絡人組連結上的擴展屬性檢索組 ID。 鏈接呈現與以下調用Ajax.ActionLink()。

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

傳遞給Ajax.ActionLink()的最後一個參數將名為 groupid 的 expando 屬性添加到連結(XHTML 相容性小寫)。

當用戶點擊瀏覽器"後退"或"前進"按鈕時,將引發導航事件並調用 navigate() 方法。 此方法更新頁面中顯示的聯繫人,以匹配與傳遞給導航方法的瀏覽器歷史記錄點對應的頁面狀態。

## <a name="performing-ajax-deletes"></a>執行 Ajax 移除

目前,要刪除連絡人,您需要按一下"刪除"鏈接,然後單擊刪除確認頁中顯示的"刪除"按鈕(參見圖 2)。 這似乎是很多頁面請求,以做一些簡單的事情,如刪除資料庫記錄。

[![刪除確認頁](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**圖 02**: 刪除確認頁([按下以檢視全尺寸影像](iteration-7-add-ajax-functionality-vb/_static/image4.png))

最好跳過刪除確認頁,直接從索引視圖中刪除連絡人。 您應該避免這種誘惑,因為採用這種方法會將應用程式打開到安全漏洞中。 通常,在調用修改 Web 應用程式狀態的操作時,不希望執行 HTTP GET 操作。 執行刪除時,要執行 HTTP POST,或者更好的是執行 HTTP DELETE 操作。

"刪除"链接包含在"連絡人列表"部分中。 清單 6 中包含連絡人清單部分的更新版本。

**清單 6 - 檢視\聯絡人清單.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

刪除連結呈現與以下調用 Ajax.ImageActionLink() 方法:

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> Ajax.ImageActionLink()不是mVCASP.NET標準部分。 Ajax.ImageActionLink()是聯絡人管理員專案中包括的自定義幫助器方法。

AjaxOptions 參數有兩個屬性。 首先,"確認"屬性用於顯示彈出的 JavaScript 確認對話方塊。 其次,HttpMethod 屬性用於執行 HTTP DELETE 操作。

清單7包含已添加到聯繫人控制器的新 AjaxDelete() 操作。

**清單7 - 控制器\聯絡控制器.vb(Ajax刪除)**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete() 操作使用 AcceptVerbs 屬性進行修飾。 此屬性可防止調用操作,但 HTTP DELETE 操作以外的任何 HTTP 操作除外。 特別是,您不能使用 HTTP GET 呼叫此操作。

刪除資料庫記錄後,需要顯示不包含已刪除記錄的聯繫人的更新清單。 AjaxDelete() 方法傳回聯絡人清單部分和更新的連絡人清單。

## <a name="summary"></a>總結

在此反覆運算中,我們將 Ajax 功能添加到我們的聯繫人管理器應用程式中。 我們使用Ajax來提高應用程式的回應性和性能。

首先,我們重構了 Index 視圖,以便單擊聯繫人組不會更新整個檢視。 相反,按一下聯繫人組只會更新聯繫人清單。

接下來,我們使用 jQuery 動畫效果淡入淡出並淡入聯繫人清單中。 向 Ajax 應用程式添加動畫可用於向應用程式的使用者提供等效的瀏覽器進度列。

我們還向 Ajax 應用程式添加了瀏覽器歷史記錄支援。 我們允許使用者單擊瀏覽器"後退"和"前進"按鈕以更改"索引"視圖的狀態。

最後,我們創建了一個支援 HTTP DELETE 操作的刪除連結。 通過執行 Ajax 刪除,我們允許使用者刪除資料庫記錄,而無需使用者請求額外的刪除確認頁。

> [!div class="step-by-step"]
> [上一步](iteration-6-use-test-driven-development-vb.md)
