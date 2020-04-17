---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 伺服器控制 |微軟文件
author: rick-anderson
description: ASP.NET 2.0 在許多方面增強了伺服器控件。 在本模組中,我們將介紹ASP.NET 2.0 和 Visual Studio 200 的方式的一些體系結構更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543739"
---
# <a name="server-controls"></a>伺服器控制項

由[微軟](https://github.com/microsoft)

> ASP.NET 2.0 在許多方面增強了伺服器控件。 在本模組中,我們將介紹ASP.NET 2.0 和Visual Studio 2005處理伺服器控制項的方式的一些體系結構更改。

ASP.NET 2.0 在許多方面增強了伺服器控件。 在本模組中,我們將介紹ASP.NET 2.0 和Visual Studio 2005處理伺服器控制項的方式的一些體系結構更改。

## <a name="view-state"></a>檢視狀態

ASP.NET 2.0 中視圖狀態的主要變化是大小顯著減小。 考慮一個只有"日曆"控制件的頁面。 下面是ASP.NET 1.1 中的視圖狀態。

[!code-css[Main](server-controls/samples/sample1.css)]

現在,下面是ASP.NET 2.0中相同頁面上的視圖狀態。

[!code-css[Main](server-controls/samples/sample2.css)]

這是一個相當重大的變化,考慮到視圖狀態在線上來回移動,此更改可以顯著提高開發人員的性能。 視圖狀態大小的減小主要是由於我們在內部處理它的方式。 請記住,檢視狀態是 Base64 編碼字串。 為了更好地瞭解 ASP.NET 2.0 中視圖狀態的變化,讓我們從上面的示例中查看解碼的值。

下面是已解碼的 1.1 檢視狀態:

[!code-css[Main](server-controls/samples/sample3.css)]

這可能看起來有點胡言亂語,但這裡有一個模式。 在ASP.NET 1.x 中,我們使用單個字元&lt;&gt;來標識 數據類型並使用字元分隔值。 上面的檢視狀態示例中的「t」表示三重。 三重清單包含一對陣列清單("l"表示陣列清單)。其中一個陣列清單包含一個 Int32 ("i"),其值為 1,另一個包含另一個 Triplet。 三重包含一對陣列清單等。需要記住的重要的事情是,我們使用包含對的三腳架,我們通過字母識別數據類型,並使用和&lt;&gt;字元作為分隔符。

在ASP.NET 2.0 中,解碼的視圖狀態看起來有點不同。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

您應該注意到解碼視圖狀態的外觀發生巨大變化。 此更改具有多個體系結構基礎。 ASP.NET 1.x 中的檢視狀態使用 LosFormatter 對資料進行序列化。 在 2.0 中,我們使用新的 Object StateFormatter 類。 此類是專門為幫助檢視狀態和控制狀態的序列化和反序列化而設計的。 (下一節將介紹控制狀態。通過改變序列化和反序列化的方法,可以帶來許多好處。 其中最戲劇性的是,與使用文本Writer的LosFormatter不同,ObjectStateFormatter使用二進制寫入器。 這允許ASP.NET 2.0 儲存一系列位元組而不是位元串的視圖狀態。 以整數為例。 在ASP.NET 1.1 中,整數需要4個字節的視圖狀態。 在ASP.NET 2.0 中,相同的整數只需要1個字節。 進行了其他增強,以減少存儲的視圖狀態量。 例如,DateTime 值現在使用TickCount而不是字串進行存儲。

似乎所有這一切還不夠,特別注意的是,在 1.x 中,視圖狀態的最大消費者之一是 DataGrid 和類似的控制項。 控件(如檢視狀態所在的 DataGrid)的一個主要缺點是,它通常包含大量重複的資訊。 在ASP.NET 1.x 中,重複的資訊只是一遍又一遍地存儲,導致視圖狀態膨脹。 在 ASP.NET 2.0 中,我們使用新的 IndexedString 類來存儲此類數據。 如果字串重複,我們只需將索引String 和索引的令牌存儲在索引String 對象的運行表中。

## <a name="control-state"></a>控制狀態

開發人員對檢視狀態的主要抱怨之一是它添加到 HTTP 負載的大小。 如前所述,視圖狀態的最大消費者之一是DataGrid控件。 為了避免 DataGrid 生成的大量檢視狀態,許多開發人員只是禁用該控制件的視圖狀態。 不幸的是,這個解決方案並不總是一個好的。 ASP.NET 1.x 中的檢視狀態不僅包含控件正確功能所需的數據。 它還包含有關控制者的 UI 的狀態的資訊。 這意味著,如果要允許在 DataGrid 上進行分頁,則必須啟用檢視狀態,即使您不需要檢視狀態包含的所有 UI 資訊也是如此。 這是一個全有或全無的情況。

在ASP.NET 2.0中,控制狀態通過引入控制狀態很好地解決了該問題。 控件狀態包含控制式正確功能絕對必要的資料。 與視圖狀態不同,無法禁用控件狀態。 因此,必須嚴格控制存儲在受控狀態的數據。

> [!NOTE]
> 控制項狀態與\_\_「檢視狀態隱藏窗體」欄位中的檢視狀態一起保留。

此視頻是視圖狀態和控制狀態的演練。

![](server-controls/_static/image1.png)

[開啟全螢幕視訊](server-controls/_static/state1.wmv)

為了使伺服器控制件讀取和寫入以控制狀態,必須執行三個步驟。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>第一步:呼叫寄存器需求控制狀態方法

註冊需求控制狀態方法ASP.NET通知控件需要保持控制狀態。 它採用類型控制(即正在註冊的控制項)的一個參數。

請務必注意,註冊不會從請求持續到請求。 因此,如果控件要保留控制狀態,則必須在每個請求上調用此方法。 建議在 OnInit 中調用該方法。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>第二步:重寫儲存控制狀態

自上次回帖以來,SaveControlState 方法保存控制件的控制狀態更改。 它返回表示控件狀態的物件。

## <a name="step-3-override-loadcontrolstate"></a>步驟 3:覆蓋負載控制狀態

LoadControlState 方法將保存的狀態載入到控制項中。 該方法採用一種類型 Object 的參數,該參數保存控制項的保存狀態。

## <a name="full-xhtml-compliance"></a>完全 XHTML 合規性

任何 Web 開發人員都知道標準在 Web 應用程式中的重要性。 為了維護基於標準的開發環境,ASP.NET 2.0 完全符合 XHTML 標準。 因此,所有標記都根據支援 HTML 4.0 或更高程度的瀏覽器中的 XHTML 標準進行呈現。

ASP.NET 1.1 中的 DOCTYPE 定義如下:

[!code-html[Main](server-controls/samples/sample6.html)]

在 ASP.NET 2.0 中,預設的 DOCTYPE 定義如下所示:

[!code-html[Main](server-controls/samples/sample7.html)]

如果選擇,您可以通過設定檔中的 xhtml 一致性節點更改預設 XHTML 合規性。 例如,Web.config 檔中的以下節點將 XHTML 符合性更改為 XHTML 1.0 嚴格:

[!code-xml[Main](server-controls/samples/sample8.xml)]

如果選擇,還可以配置ASP.NET以使用 ASP.NET 1.x 中使用的舊配置,如下所示:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>使用配接器進行自我調整

在 ASP.NET 1.x 中&lt;,配置檔&gt;包含填充 HttpBrowser 功能物件的瀏覽器 Cap 節。 此物件允許開發人員確定正在發出特定請求的設備並適當地呈現代碼。 在 ASP.NET 2.0 中,模型已改進,現在使用新的 ControlAdapter 類。 ControlAdapter 類覆蓋控制件生命週期中的事件,並控制基於使用者代理功能的控制件的呈現。 特定使用者代理的功能由存儲在 c:_windows_microsoft.net_framework_v2.0 中的瀏覽器定義檔(具有 .browser 檔副檔名的檔案)定義。\* \*[CONFIG]瀏覽器\* \*

> [!NOTE]
> ControlAdapter 類是一個抽象類。

與 1.x&lt;中的&gt;瀏覽器 Cap 節類似,瀏覽器定義檔案使用正則運算式來分析使用者代理字串以識別請求的瀏覽器。 它們定義該使用者代理的特定功能。 控件適配器通過渲染方法呈現控件。 因此,如果重寫 Render 方法,則不應在基類上調用 Render。 這樣做可能會導致渲染發生兩次,一次用於適配器,一次用於控件本身。

## <a name="developing-a-custom-adapter"></a>開發自訂介面卡

您可以通過從 ControlAdapter 繼承來開發自己的自訂適配器。 此外,在頁面需要適配器的情況下,可以從抽象類 PageAdapter 繼承。 控制項映射到自訂配接器是透過瀏覽器定義檔中的&lt;控制項配接器&gt;元素完成的。 例如,瀏覽器定義檔案中的以下 XML 將選單控制元件映射到 MenuAdapter 類別:

[!code-html[Main](server-controls/samples/sample10.html)]

使用此模型,控件開發人員很容易定位特定設備或瀏覽器。 對於開發人員來說,完全控制每個設備上的頁面呈現方式也非常簡單。

## <a name="per-device-rendering"></a>每裝置渲染

ASP.NET 2.0 中的伺服器控制項屬性可以使用特定於瀏覽器的前置碼按裝置指定。 例如,下面的代碼將更改標籤的文本,具體取決於用於瀏覽頁面的設備。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

當包含此標籤的頁面從 Internet Explorer 瀏覽時,標籤將顯示文本,上面寫著"您正在從 Internet 資源管理器流覽」。。 當從 Firefox 瀏覽頁面時,標籤將顯示文本「您正在從 Firefox 瀏覽」。 從任何其他設備瀏覽頁面時,將顯示「您正在從未知設備瀏覽」。 可以使用此特殊語法指定任何屬性。

## <a name="setting-focus"></a>設定焦點

ASP.NET 1.x 開發人員經常詢問如何將初始焦點放在特定控制項。 例如,在登錄頁上,讓使用者 ID 文本框在頁面首次載入時獲取焦點非常有用。 在ASP.NET 1.x 中,執行此操作需要編寫一些用戶端腳本。 儘管此類腳本是一項瑣碎的任務,但由於 SetFocus 方法,ASP.NET 2.0 中不再需要它。 SetFocus 方法採用一個參數,指示應接收焦點的控制項。 此參數可以是控制項的客戶端 ID 作為字串,也可以是 Server 控制件的名稱作為控制項物件。 例如,要將初始焦點設定為頁面首次載入時稱為 txtUserID 的 TextBox 控制項\_,請向頁面載入新增以下代碼:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

- 或

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 使用 Webresource.axd 處理程式(前面討論)來呈現設置焦點的用戶端函數。 用戶端函數的名稱是 WebForm\_自動焦點,如下所示:

[!code-html[Main](server-controls/samples/sample14.html)]

或者,可以使用控制項的 Focus 方法將初始焦點設定為該控制項。 Focus 方法派生自 Control 類,可用於所有ASP.NET 2.0 控件。 當發生驗證錯誤時,還可以將焦點設置為特定控制項。 稍後將介紹這一點。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 中的新伺服器控制項

以下是 ASP.NET 2.0 中的新伺服器控制件。 我們將在後面的模組中更詳細地介紹其中一些內容。

## <a name="imagemap-control"></a>影像對應控制項

ImageMap 控制項允許您向影像添加熱點,該影像可以啟動帖子或導航到 URL。 有三種類型的熱點可用;圓熱點、矩形熱點和多邊形熱點。 熱點透過 Visual Studio 中的集合編輯器添加,或在代碼中以程式設計方式添加。 沒有可用於在圖像上繪製熱點的用戶介面。 必須聲明性地指定熱點的座標、大小或半徑。 設計器中也沒有熱點的可視表示形式。 如果熱點配置為導航到 URL,則 URL 將通過熱點的 NavigateUrl 屬性指定。 在後回熱點的情況下,PostBackValue 屬性允許您傳遞後回的字串,該字串可以在伺服器端代碼中檢索。

![視覺化工作室中的熱點集合編輯器](server-controls/_static/image1.jpg)

**圖 1**: 視覺化工作室中的熱點集合編輯器

## <a name="bulletedlist-control"></a>項目符號清單控制

項目符號清單「控制件是一個項目符號清單,可以輕鬆綁定數據。 清單可以通過「項目符號樣式」屬性排序(編號)或無序排序。 清單中的每個項都由 ListItem 物件表示。

![視覺化工作室中的項目符號清單控制](server-controls/_static/image1.gif)

**圖 2**: 視覺化工作室中的項目清單控制

## <a name="hiddenfield-control"></a>隱藏欄位控制

HiddenField 控制件向頁面添加隱藏表單欄位,其值在伺服器端代碼中可用。 隱藏窗體欄位的值通常預計在後背之間保持不變。 但是,惡意使用者可能會在回發佈之前更改該值。 如果發生這種情況,"隱藏欄位"控制件將引發"值更改"事件。 如果在 HiddenField 控制件中具有敏感資訊,並且希望確保資訊保持不變,則應在代碼中處理 Value"更改"事件。

## <a name="fileupload-control"></a>檔案上傳控制

ASP.NET 2.0 中的 FileUpload 控制件使得可以通過 ASP.NET 頁面將檔上傳到 Web 伺服器成為可能。 此控制項與 ASP.NET 1.x HtmlInputFile 類非常相似,但有一些例外。 在 ASP.NET 1.x 中,建議將「已發布檔」屬性檢查為 null,以確定您是否具有良好的檔。 ASP.NET 2.0 中的 FileUpload 控件添加了一個新的 HasFile 屬性,您可以將其用於同一目的,並且效率更高一些。

已發布檔屬性仍可用於訪問 HttpPostedFile 物件,但 HttpPostedFile 的某些功能現在可透過 FileUpload 控制檔在本質上可用。 例如,要將上載的檔保存在 ASP.NET 1.x 中,請調用 HttpPostedFile 物件上的 SaveAs 方法。 使用 ASP.NET 2.0 中的 FileUpload 控制項,您將在 FileUpload 控制項本身上調用 SaveAs 方法。

2.0 行為(可能是最重要的更改)的另一個重要變化是,在保存整個上載的檔之前,不再需要將整個上載的檔載入到記憶體中。 在 1.x 中,上傳的任何檔在寫入磁碟之前都完全保存到記憶體中。 此體系結構可防止上載大型檔。

在 ASP.NET 2.0 中,HTTPRuntime 元素的請求長度磁碟閾值屬性允許您設定在寫入磁碟之前在記憶體中存儲緩衝區中的數量。

**重要提示**:MSDN 文件(和其他地方的文檔)指定此值以位元組為單位(不是千位元組),預設值為 256。 該值實際上以千位元組為單位指定,預設值為 80。 通過預設值 80K,我們確保緩衝區不會最終位於大型物件堆上。

## <a name="wizard-control"></a>向導控制

遇到ASP.NET開發人員在嘗試使用面板在一系列「頁面」中收集資訊或從一個頁面傳輸到一個頁面時遇到這樣的常見情況。 很多時候,這種努力是令人沮喪的,而且非常耗時。 新的嚮導控件通過在使用者熟悉的嚮導介面中允許線性和非線性步驟來解決問題。 嚮導控制項以一系列步驟顯示輸入窗體。 每個步驟都是控件的 StepType 屬性指定的特定類型。 可用的步驟類型如下:

| **步長類型** | **說明** |
| --- | --- |
| Auto | 嚮導根據步驟層次結構中的位置自動確定步驟的類型。 |
| Start | 第一步,通常用於提出介紹性陳述。 |
| 步驟 | 正常步驟。 |
| [完成] | 最後一步,通常用於顯示一個按鈕來完成嚮導。 |
| [完成] | 顯示傳達成功或失敗的資訊。 |

> [!NOTE]
> 嚮導控制件使用ASP.NET控制狀態追蹤其狀態。 因此,啟用檢視狀態屬性可以設置為 false,而不會造成任何損害。

此視頻是嚮導控件的演練。

![](server-controls/_static/image2.png)

[開啟全螢幕視訊](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>本地化控制

當地語系化控制項類似於文字控制項。 但是,當地語系化控制項具有一個**Mode**屬性,用於控制如何向其添加標記。 Mode 屬性支援以下值:

| **Mode** | **說明** |
| --- | --- |
| 轉換 | 標記根據發出請求的瀏覽器的協議進行轉換。 |
| 直通 | 標記將呈現為"正樣"。 |
| 編碼 | 新增到控制項的標記使用 HtmlEncode 進行編碼。 |

## <a name="multiview-and-view-controls"></a>多檢視及檢視控制項

MultiView 控件充當檢視控制件的容器,檢視控制項充當其他控制項的容器(與面板控制項類似)。 MultiView 控制件中的每個檢視都由單個檢視控制項表示。 MultiView 中的第一個檢視控件是視圖 0,第二個視圖 1 等。您可以通過指定 MultiView 控制件的 ActiveViewIndex 來切換檢視。

## <a name="substitution-control"></a>替代控制

替換控制項與ASP.NET快取一起使用。 如果要利用緩存,但具有必須在每個請求上更新頁面的某些部分(換句話說,免除緩存的頁面部分),則替換元件提供了一個很好的解決方案。 控件實際上不會自行呈現任何輸出。 相反,它綁定到伺服器端代碼中的方法。 請求頁面時,將調用該方法,並呈現返回的標記來代替替換控制項。

透過**MethodName**屬性指定替換控制項的結合的方法。 該方法必須滿足以下條件:

- 它必須是靜態(在VB中共用)方法。
- 它接受 HTTPContext 類型的一個參數。
- 它返回一個字串,表示應替換頁面上的控件的標記。

替換控制項無法修改頁面上的任何其他控制項,但它確實可以透過其參數存取目前 HTTPContext。

## <a name="gridview-control"></a>格線檢視控制

GridView 控件是 DataGrid 控制件的替換。 此控件將在後面的模組中更詳細地介紹。

## <a name="detailsview-control"></a>詳細資訊檢視控制項

"詳細資訊檢視"控制件允許您從資料源顯示單個記錄,並對其進行編輯或刪除。 在後面的模組中更詳細地介紹它。

## <a name="formview-control"></a>表單檢視控制項

FormView 控制項用於在可配置的界面中顯示來自資料源的單個記錄。 在後面的模組中更詳細地介紹它。

## <a name="accessdatasource-control"></a>存取資料來源控制

AccessDataSource 控制項用於資料綁定 Access 資料庫。 在後面的模組中更詳細地介紹它。

## <a name="objectdatasource-control"></a>物件資料來源控制

ObjectDataSource 控制項用於支援三層體系結構,以便控制項可以將資料綁定到中介層業務物件,而不是控制項直接綁定到資料源的雙層模型。 稍後將在後面的模組中更詳細地討論它。

## <a name="xmldatasource-control"></a>XmlDataSource 控制

XmlDataSource 控制項用於結合XML資料來源的資料。 在後面的模組中更詳細地介紹它。

## <a name="sitemapdatasource-control"></a>站台對應資料來源控制

SiteMapDataSource 控制件基於網站地圖為網站導航控制件提供數據綁定。 稍後將在後面的模組中更詳細地討論它。

## <a name="sitemappath-control"></a>站台地圖路徑控制

SiteMapPath 控制項顯示一系列導航連結,通常稱為痕跡。 在後面的模組中更詳細地介紹它。

## <a name="menu-control"></a>功能表控制項

"選單"控制項使用 DHTML 顯示動態功能表。 在後面的模組中更詳細地介紹它。

## <a name="treeview-control"></a>TreeView 控制項

TreeView 控件用於顯示數據的分層樹視圖。 在後面的模組中更詳細地介紹它。

## <a name="login-control"></a>登入控制

登錄控件提供了登錄到網站的機制。 在後面的模組中更詳細地介紹它。

## <a name="loginview-control"></a>LoginView 控制項

登錄視圖控制件允許根據使用者的登錄狀態顯示不同的範本。 在後面的模組中更詳細地介紹它。

## <a name="passwordrecovery-control"></a>密碼修復控制

密碼恢復控制項用於檢索ASP.NET應用程式的使用者忘記的密碼。 在後面的模組中更詳細地介紹它。

## <a name="loginstatus"></a>LoginStatus

登錄狀態控制項顯示使用者的登錄狀態。 在後面的模組中更詳細地介紹它。

## <a name="loginname"></a>LoginName

登錄名稱控制件在登入ASP.NET應用程式後顯示使用者的使用者名。 在後面的模組中更詳細地介紹它。

## <a name="createuserwizard"></a>建立使用者精靈

CreateUserWizard 是一個可配置的嚮導,它使用戶能夠創建ASP.NET成員資格帳戶,供ASP.NET應用程式使用。 在後面的模組中更詳細地介紹它。

## <a name="changepassword"></a>ChangePassword

更改密碼控制項允許使用者更改其ASP.NET應用程式的密碼。 在後面的模組中更詳細地介紹它。

## <a name="various-webparts"></a>各種 Web 組件

ASP.NET 2.0 船舶與各種 Web 部件。 這些將在後面的模組中詳細介紹。
