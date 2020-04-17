---
uid: mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
title: 反覆運算#2 = 使應用程式看起來不錯 (VB) |微軟文件
author: rick-anderson
description: 在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f65cb436-e493-46fd-9608-384b27385aa1
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-2-make-the-application-look-nice-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a97958db442c48bd696f6414f7226127984bc34
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542426"
---
# <a name="iteration-2--make-the-application-look-nice-vb"></a>反覆項目 #2 – 美化應用程式外觀 (VB)

由[微軟](https://github.com/microsoft)

[下載代碼](iteration-2-make-the-application-look-nice-vb/_static/contactmanager_2_vb1.zip)

> 在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>建構 MVC 應用程式 (VB) ASP.NET連絡人管理

在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。 透過聯絡人管理員應用程式,您可以儲存連絡人資訊(姓名、電話號碼和電子郵件位址)以儲存人員清單。

我們通過多次反覆運算構建應用程式。 每次反覆運算時,我們都會逐步改進應用程式。 此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。

- 反覆運算#1 = 創建應用程式。 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。

- 反覆運算#2 = 使應用程式看起來不錯。 在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。

- 反覆運算#3 = 添加表單驗證。 在第三個反覆運算中,我們添加基本表單驗證。 我們防止人們在未填寫所需表單欄位的情況下提交表單。 我們還驗證電子郵件地址和電話號碼。

- 反覆運算#4 = 使應用程式鬆散耦合。 在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。 例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。

- 反覆運算#5 = 創建單元測試。 在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。 我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。

- 反覆運算#6 = 使用測試驅動開發。 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,我們添加聯繫人組。

- 反覆運算#7 = 添加 Ajax 功能。 在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。

## <a name="this-iteration"></a>此反覆運算

此反覆運算的目標是改進聯繫人管理器應用程式的外觀。 目前,連絡人管理器使用預設ASP.NET MVC 檢視母版頁和級聯樣式表(參見圖 1)。 這些看起來並不壞,但我不希望聯繫人管理器看起來像所有其他ASP.NET MVC 網站。 我想用自定義檔替換這些檔。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image1.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image1.png)

**圖 01**: ASP.NET mVC 應用程式的預設外觀([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image2.png))

在此反覆運算中,我討論了改進應用程式可視化設計的兩種方法。 首先,我將向您展示如何利用ASP.NET MVC 設計庫下載免費ASP.NET MVC 設計範本。 ASP.NET MVC 設計庫使您能夠創建專業 Web 應用程式,而無需進行任何工作。

我決定不再使用聯繫人管理器應用程式ASP.NET MVC 設計庫中的範本。 相反,我有一個專業的設計公司創造的定製設計。 在本教程的第二部分中,我解釋了我如何與一家專業設計公司合作,創建最終ASP.NET MVC 設計。

## <a name="the-aspnet-mvc-design-gallery"></a>ASP.NET MVC 設計庫

ASP.NET MVC 設計庫是微軟提供的免費資源。 ASP.NET MVC 函式庫位於以下位址:

[https://www.asp.net/mvc/gallery](https://www.asp.net/mvc/gallery)

ASP.NET MVC 設計庫託管一組免費網站設計,這些設計專為ASP.NET MVC 專案中使用而創建。 設計由社區成員上傳。 參觀畫廊的參觀者可以投票選出他們最喜歡的設計(參見圖2)。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image2.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image3.png)

**圖02**: ASP.NET MVC 設計函式庫 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image4.png))

在寫本教程時,畫廊中最受歡迎的設計是大衛·豪瑟設計的10月。 您可以通過完成以下步驟,為 mVC 專案ASP.NET使用此設計:

1. 按下 **「下載**」按鈕將 10 月.zip 檔案下載到您的電腦。
2. 右鍵按一下下載的 10 月.zip 檔,然後按下 **「取消阻止」** 按鈕(參見圖 3)。
3. 解壓縮檔到名為 10 月的資料夾。
4. 從 10 月資料夾中的 DesignTemplate 資料夾中選擇所有檔,右鍵單擊檔,然後選擇功能表選項 **「複製**」。。
5. 右鍵按一下可視化工作室解決方案資源管理器視窗中的 ContactManager 專案節點,然後選擇選單選項 **「粘貼**」(參見圖 4)。
6. 選擇「視覺化工作室」選單選項 **「編輯、尋找與取代」、「快速取代**」,*並將其替換為**聯絡人管理員*(參見圖 5)。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image3.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image5.png)

**圖 03**: 取消封鎖到 Web 下載的檔案 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image6.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image4.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image7.png)

**圖 04**: 解決方案資源管理員中的覆寫檔案 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image8.png))

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image5.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image9.png)

**圖 05**: 將 [專案名稱] 取代為聯絡人管理員 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image10.png))

完成這些步驟後,Web 應用程式將使用新設計。 圖 6 中的頁面說明了使用 10 月設計的聯繫人管理器應用程式的外觀。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image6.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image11.png)

**圖 06**: 使用 10 月樣本聯繫經理 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image12.png))

## <a name="creating-a-custom-aspnet-mvc-design"></a>建立自訂ASP.NET MVC 設計

ASP.NET MVC 設計庫具有多種設計風格。 庫為您提供了一種無痛的方式來自定義ASP.NET MVC 應用程式的外觀。 當然,畫廊有很大的優勢是完全自由的。

但是,您可能需要為您的網站創建完全獨特的設計。 在這種情況下,與網站設計公司合作是有意義的。 我決定採用這種方法來設計聯繫人管理器應用程式。

我壓縮了反覆運算#1的聯繫人管理器,並將項目發送給了設計公司。 他們沒有視覺工作室(羞辱他們! 他們能夠從網站免費下載 Microsoft 視覺化[https://www.asp.net](https://www.asp.net)Web 開發人員,並在可視化 Web 開發人員中打開聯絡人管理器應用程式。 幾天后,他們製作了圖7中的設計。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image7.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image13.png)

**圖07**: ASP.NET MVC 連絡人管理員設計 ([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image14.png))

新的設計由兩個主要文件組成:一個新的級聯樣式表檔和一個新的視圖母版頁檔。 檢視母版頁包含ASP.NET MVC 應用程式中的檢視的佈局和共用內容。 例如,檢視母版頁包括圖 7 中顯示的標題、導航選項卡和頁腳。 我用新的 Site.Master 檔在「視圖」和「共用」資料夾中重寫了現有的 Site.Master 視圖母版頁,

設計公司還創建了一個新的級聯樣式表和一組圖像。 我把這些新檔放在內容資料夾中,並覆蓋了現有的 Site.css 檔。 應將所有靜態內容放在"內容"資料夾中。

請注意,連絡人管理器的新設計包括用於編輯和刪除連絡人的圖像。 連絡人的 HTML 表中,每個連絡人旁邊都會顯示「編輯」和「刪除」圖像。

最初,這些連結是使用 HTML 呈現的。操作連結() 說明程式如下所示:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample1.aspx)]

Html.ActionLink() 方法不支援影像(出於安全原因,方法 HTML 對連結文本進行編碼)。 因此,我將對 Html.ActionLink() 的呼叫為對 Url.Action() 的呼叫,如下所示:

[!code-aspx[Main](iteration-2-make-the-application-look-nice-vb/samples/sample2.aspx)]

Html.ActionLink() 方法呈現整個 HTML 超連結。 另一方面,Url.Action() 方法只呈現&lt;&gt;沒有 標記的 URL。

此外,請注意,新設計包括所選選項卡和未選中選項卡。 例如,在圖 8 中,選擇了 **「創建新聯繫人」** 選項卡,並且未選擇「**我的聯繫人**」選項卡。

[![[New Project] \(新增專案\) 對話方塊](iteration-2-make-the-application-look-nice-vb/_static/image8.jpg)](iteration-2-make-the-application-look-nice-vb/_static/image15.png)

**圖 08**: 選擇與未選取的選項卡([按下以檢視全尺寸影像](iteration-2-make-the-application-look-nice-vb/_static/image16.png))

為了支援呈現所選選項卡和未選中選項卡,我創建了一個名為 MenuItemHelper 的自定義 HTML 説明程式。 此說明&lt;器方法呈現一個&gt;li 標&lt;記或 li&gt;class=" 選定"標記,具體取決於目前控制器和操作是否與傳遞給説明程式的控制器和操作名稱相對應。 功能表項目説明程式的代碼包含在清單 1 中。

**清單1 = 說明者\選單專案說明程式.vb**

[!code-vb[Main](iteration-2-make-the-application-look-nice-vb/samples/sample3.vb)]

MenuItemHelper 在內部使用 TagBuilder&lt;&gt;類來 建構 li HTML 標籤。 TagBuilder 類是一個非常有用的實用程式類,您可以隨時構建新的 HTML 標記時使用該類。 它包括添加屬性、添加 CSS 類、生成 Id 和修改標記的內部 HTML 的方法。

## <a name="summary"></a>總結

在此反覆運算中,我們改進了ASP.NET MVC 應用程式的可視化設計。 首先,您將被介紹到ASP.NET MVC 設計庫。 您學習了如何從ASP.NET MVC 設計庫中下載免費設計範本,這些範本可用於ASP.NET MVC 應用程式中。

接下來,我們將討論如何通過修改預設級聯樣式表檔和母版視圖頁檔來創建自定義設計。 為了支援新設計,我們不得不對我們的聯繫人管理器應用程式進行一些小的更改。 例如,我們添加了一個名為 MenuItemHelper 的新 HTML 説明程式,該助手顯示所選和未選中的選項卡。

在下一個反覆運算中,我們將處理非常重要的驗證主題。 我們將驗證代碼添加到我們的應用程式中,以便使用者在未提供所需值(如人員姓名和姓氏)的情況下無法創建新聯繫人。

> [!div class="step-by-step"]
> [前一個](iteration-1-create-the-application-vb.md)
> [下一個](iteration-3-add-form-validation-vb.md)
