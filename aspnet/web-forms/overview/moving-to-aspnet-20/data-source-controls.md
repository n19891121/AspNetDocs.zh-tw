---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 資料來源控制 |微軟文件
author: rick-anderson
description: ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。 然而,它並不像它本來可以的那麼使用者友好。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: 2b4302b509af57dc5d9db9de9ee824df767d0737
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81540216"
---
# <a name="data-source-controls"></a>資料來源控制項

由[微軟](https://github.com/microsoft)

> ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。 然而,它並不像它本來可以對使用者友好。 它仍然需要大量的代碼才能從中獲得許多有用的功能。 這就是 1.x 中所有數據訪問努力中的模型。

ASP.NET 1.x 中的 DataGrid 控制件標誌著 Web 應用程式中數據存取的重大改進。 然而,它並不像它本來可以對使用者友好。 它仍然需要大量的代碼才能從中獲得許多有用的功能。 這就是 1.x 中所有數據訪問努力中的模型。

ASP.NET 2.0 部分使用數據源控件解決了這個問題。 ASP.NET 2.0 中的數據來源控制項為開發人員提供了用於檢索資料、顯示數據和編輯數據的聲明性模型。 數據源控件的目的是向數據綁定控件提供數據一致的表示形式,而不管數據源如何。 ASP.NET 2.0 中資料源控制項的核心是 DataSourceControl 抽象類。 DataSourceControl 類提供了 IDataSource 介面和 IListSource 介面的基本實現,後者允許您將資料來源控制項指定為數據綁定控制項的 DataSource(透過稍後討論的新 DataSourceId 屬性),並將其中的數據公開為清單。 數據源控制項每個資料清單都公開為 DataSourceView 物件。 IDataSource 介面提供了對 DataSourceView 實例的訪問。 例如,GetViewNames 方法傳回 ICollection,允許您枚舉與特定資料來源控制項關聯的 DataSourceViews,GetView 方法允許您按名稱存取特定的 DataSourceView 實例。

數據源控件沒有用戶介面。 它們作為伺服器控制項實現,以便它們可以支援聲明性語法,以便根據需要存取頁面狀態。 數據來源控制項不向客戶端呈現任何 HTML 標籤。

> [!NOTE]
> 稍後您將看到,使用數據源控件還可以獲得緩存好處。

## <a name="storing-connection-strings"></a>儲存連線字串

在研究如何配置數據源控件之前,我們應該在有關連接字串ASP.NET 2.0 中介紹新功能。 ASP.NET 2.0 在設定檔中引入了一個新部分,允許您輕鬆儲存可在運行時動態讀取的連接字串。 連接&lt;字串&gt;部份便於儲存連接字串。

下面的代碼段添加了一個新的連接字串。

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;與&gt;appSettings 部分一&lt;樣, 連接&gt;字串 部分顯示在&lt;配置檔中的 system.web&gt;部分之外。

要使用此連接字串,可以在設定伺服器控制項的 ConnectString 屬性時使用以下語法。

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

還可以&lt;加密&gt;連接 字串部分,以便不公開敏感資訊。 這一能力將在後面的模組中介紹。

## <a name="caching-data-sources"></a>快取資料來源

每個 DataSourceControl 提供四個屬性來配置緩存;啟用快取、快取持續時間、緩存過期策略和快取金鑰依賴性。

## <a name="enablecaching"></a>開啟快取

啟用快取是一個布林屬性,用於確定是否為資料源控制項啟用緩存。

## <a name="cacheduration-property"></a>快取持續時間屬性

"快取時間"屬性設定快取保持有效的秒數。 將此屬性設置為**0**會導致緩存保持有效,直到顯式失效。

## <a name="cacheexpirationpolicy-property"></a>快取過期政策屬性

快取過期政策屬性可以設定為**絕對**或**滑動**。 將其設置為「絕對」意味著緩存數據的最大時間是 CacheDuration 屬性指定的秒數。 通過將它設置為「滑動」,執行每個操作時將重置過期時間。

## <a name="cachekeydependency-property"></a>快取金鑰相依屬性

如果為 CacheKey 依賴項屬性指定了字串值,ASP.NET將基於該字串設置新的緩存依賴項。 這允許您透過簡單地更改或刪除 CacheKey 依賴項來顯式使緩存無效。

**重要提示**:如果啟用了類比,並且對資料源和/或數據內容的訪問基於用戶端標識,則建議通過設置啟用緩存設置為 False 來禁用緩存。 如果在此方案中啟用了緩存,並且最初請求數據的使用者以外的使用者發出請求,則不會強制執行對數據源的授權。 數據將僅從緩存中提供。

## <a name="the-sqldatasource-control"></a>SqlDataSource 控制項

SqlDataSource 控制件允許開發人員存取儲存在支援ADO.NET的任何關係資料庫中的數據。 它可以使用 System.Data.SqlClient 提供程式訪問 SQL Server 資料庫、System.Data.OleDb 提供程式、系統.Data.Odbc 提供程式或 System.Data.OracleClient 提供程式來造訪 Oracle。 因此,SqlDataSource 當然不僅用於訪問 SQL Server 資料庫中的數據。

為了使用 SqlDataSource,您只需為 ConnectString 屬性提供一個值,並指定 SQL 命令或儲存過程。 SqlDataSource 控制項負責使用底層ADO.NET體系結構。 它打開連接,查詢數據源或執行存儲過程,返回數據,然後為您關閉連接。

> [!NOTE]
> 由於 DataSourceControl 類會自動為您關閉連接,因此它應該減少因資料庫連接洩漏而生成的客戶呼叫數。

下面的代碼段使用儲存在配置檔中的連接字串將下拉清單控件綁定到 SqlDataSource 控制項,如上所示。

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

如上所述,SqlDataSource 的 DataSourceMode 屬性指定數據源的模式。 在上面的範例中,資料來源模式設置為資料閱讀器。 在這種情況下,SqlDataSource 將使用僅行和唯讀游標返回 IDataReader 物件。 返回的指定類型的物件由所使用的提供程式控制。 在這種情況下,我使用的是 Web.config&lt;檔的 connectStrings&gt;部分中指定的 System.Data.SqlClient 提供程式。 因此,返回的對象將採用 SqlDataReader 類型。 通過指定 DataSet 的 DataSourceMode 值,資料可以儲存在伺服器上的 DataSet 中。 此模式允許您添加排序、分頁等功能。如果我將 SqlDataSource 數據綁定到 GridView 控件,我會選擇 DataSet 模式。 但是,在下拉清單的情況下,數據閱讀器模式是正確的選擇。

> [!NOTE]
> 緩存 SqlDataSource 或 AccessDataSource 時,必須將 DataSourceMode 屬性設置為 DataSet。 如果使用 DataReader 的 DataSource 模式啟用快取,則會出現異常。

## <a name="sqldatasource-properties"></a>SqlDataSource 屬性

以下是 SqlDataSource 控制件的一些屬性。

### <a name="cancelselectonnullparameter"></a>取消選取的參數

布爾值,用於指定如果其中一個參數為空,是否取消選擇命令。 預設為 true。

### <a name="conflictdetection"></a>衝突偵測

在多個使用者可能同時更新數據源的情況下,衝突檢測屬性確定 SqlDataSource 控制件的行為。 此屬性計算為衝突選項枚舉的值之一。 這些值是**比較所有值**與**覆寫變更**。 如果設置為"覆蓋更改",則最後一個將數據寫入數據源的人員將覆蓋任何以前的更改。 但是,如果衝突檢測屬性設置為比較 AllValue,則為 SelectCommand 返回的列創建參數,並創建參數以在每個列中保存原始值,從而允許 SqlDataSource 確定自執行 SelectCommand 以來值是否已更改。

### <a name="deletecommand"></a>移除命令

設定或取得從資料庫中刪除行時使用的 SQL 字串。 這可以是 SQL 查詢或儲存過程名稱。

### <a name="deletecommandtype"></a>刪除指令型態

設置或獲取刪除命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。

### <a name="deleteparameters"></a>刪除參數

返回與 SqlDataSource 控制件關聯的 SqlDataSourceView 物件的 DeleteCommand 使用的參數。

### <a name="oldvaluesparameterformatstring"></a>舊值參數格式字串

此屬性用於指定原始值參數的格式,在衝突檢測屬性設置為比較AllValue的情況下。 預設值表示{0}原始值參數的名稱與原始參數相同。 換句話說,如果欄位名稱稱為 EmployID,則原始值參數將@EmployeeID為 。

### <a name="selectcommand"></a>SelectCommand

設置或獲取用於從資料庫中檢索數據的 SQL 字串。 這可以是 SQL 查詢或儲存過程名稱。

### <a name="selectcommandtype"></a>選擇指令型態

設置或獲取選擇命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。

### <a name="selectparameters"></a>選擇參數

返回與 SqlDataSource 控制件關聯的 SqlDataSource 物件的 SelectCommand 使用的參數。

### <a name="sortparametername"></a>排序參數名稱

獲取或設置在排序數據來源控制元件檢索的資料時使用的儲存過程參數的名稱。 僅當 SelectCommandType 設定為儲存過程時才有效。

### <a name="sqlcachedependency"></a>SqlCache 相依性

指定 SQL Server 快取相依項中使用的資料庫和表的分號分隔字串。 (SQL 緩存依賴項將在後面的模組中討論。

### <a name="updatecommand"></a>更新命令

設定或獲取更新資料庫中的數據時使用的 SQL 字串。 這可以是 SQL 查詢或儲存過程名稱。

### <a name="updatecommandtype"></a>更新指令型態

設置或獲取更新命令的類型,SQL 查詢(文本)或存儲過程(存儲過程)。

### <a name="updateparameters"></a>更新參數

返回與 SqlDataSource 控制件關聯的 SqlDataSourceView 物件的 UpdateCommand 使用的參數。

## <a name="the-accessdatasource-control"></a>存取資料來源控制項

AccessDataSource 控制件派生自 SqlDataSource 類,用於將資料綁定到 Microsoft Access 資料庫。 AccessDataSource 控制項的 ConnectString 屬性是唯讀屬性。 DataFile 屬性使用"連接字串"屬性,而不是使用 ConnectString 屬性來指向訪問資料庫,如下所示。

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource 將始終將基本 SqlDataSource 的提供程式名稱設置為系統.Data.OleDb,並使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供程式連接到資料庫。 不能使用 AccessDataSource 控制件連接到受密碼保護的訪問資料庫。 如果必須連接到受密碼保護的資料庫,則應使用 SqlDataSource 控制項。

> [!NOTE]
> 存儲在網站中的訪問資料庫應放在應用\_數據目錄中。 ASP.NET不允許瀏覽此目錄中的檔案。 使用 Access 資料庫時,您需要\_向應用 資料目錄授予進程帳戶"讀取和寫入"許可權。

## <a name="the-xmldatasource-control"></a>XmlDataSource 控制項

XmlDataSource 用於將資料綁定 XML 資料到資料綁定控制項。 您可以使用 DataFile 屬性結合 XML 檔,也可以使用 Data 屬性結合 XML 字串。 XmlDataSource 將 XML 屬性公開為可綁定欄位。 如果需要綁定到未表示為屬性的值,則需要使用 XSL 轉換。 您還可以使用 XPath 表示式來篩選 XML 資料。

請考慮以下 XML 檔:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

請注意,XmlDataSource 使用*人員/人員*的 XPath&lt;&gt;屬性來僅對人員 節點進行篩選。 然後,使用DataTextField屬性將數據綁定到姓氏屬性。

雖然 XmlDataSource 控制件主要用於將數據綁定到唯讀的 XML 資料,但可以編輯 XML 資料檔。 請注意,在這種情況下,自動插入、更新和刪除 XML 檔中的資訊不會像在其他數據源控制件中那樣自動發生。 相反,您必須編寫代碼才能使用 XmlDataSource 控制件的以下方法手動編輯數據。

### <a name="getxmldocument"></a>取得Xml文件

檢索包含 XmlDataSource 檢索的 XML 代碼的 XmlDocument 物件。

### <a name="save"></a>儲存

將記憶體中的 XmlDocument 儲存回資料來源。

請務必瞭解,僅滿足以下兩個條件時,Save 方法才能工作:

1. XmlDataSource 正在使用 DataFile 屬性綁定到 XML 檔案,而不是資料屬性以綁定到記憶體中的 XML 資料。
2. 不會透過『轉換』或「轉換檔」屬性指定轉換。

另請注意,當多個用戶同時調用 Save 方法時,可能會產生意外的結果。

## <a name="the-objectdatasource-control"></a>物件資料來源控制項

對於數據源控件直接與數據存儲通信的兩層應用程式而言,我們覆蓋的數據源控件是絕佳的選擇。 但是,許多實際應用程式是多層應用程式,其中數據源控件可能需要與業務物件通信,而業務物件又與數據層通信。 在這些情況下,ObjectDataSource 很好地填充了帳單。 ObjectDataSource 與源物件結合使用。 如果物件具有實例方法而不是靜態方法(在 Visual Basic 中共用),則 ObjectDataSource 控制件將創建源物件的實例,調用指定的方法,並釋放物件實例。 因此,對象必須是無狀態的。 也就是說,對象應在單個請求的範圍內獲取和釋放所有必需的資源。 您可以通過處理 ObjectDataSource 控制件的物件創建事件來控制來源物件的建立方式。 您可以建立源物件的實例,然後將 ObjectDataSourceEventArgs 類的 ObjectInstance 屬性設置為該實例。 ObjectDataSource 控制項使用在物件建立事件中建立的實體,而不是自行建立實例。

如果 ObjectDataSource 控制件的源物件公開可呼叫以檢索和修改資料的公共靜態方法(在 Visual Basic 中共用),則 ObjectDataSource 控制件將直接呼叫這些方法。 如果 ObjectDataSource 控制項必須建立源物件的實例才能進行方法呼叫,則該物件必須包括一個不採用任何參數的公共構造函數。 當 ObjectDataSource 控制件建立源物件的新實例時,它將調用此建構函數。

如果源物件不包含沒有參數的公共構造函數,則可以創建源物件的實例,該實例將由 ObjectDataSource 控制件在 ObjectCreate 事件中使用。

## <a name="specifying-object-methods"></a>指定物件方法

ObjectDataSource 控制項的來源物件可以包含任何任何數量的用於選擇、插入、更新或刪除資料的方法。 這些方法由基於方法名稱的 ObjectDataSource 控制件呼叫,使用 ObjectDataSource 控制項的 SelectMethod、插入方法、更新方法或 DeleteMethod 屬性識別。 源物件還可以包括可選的 SelectCount 方法,該方法由使用 SelectCountMethod 屬性的 ObjectDataSource 控制件標識,該方法返回數據源中物件總數的計數。 在調用 Select 方法以檢索資料來源中用於分頁時的記錄總數後,ObjectDataSource 控制件將調用 SelectCount 方法。

## <a name="lab-using-data-source-controls"></a>使用資料來源控制項的實驗室

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>練習 1 - 使用 SqlDataSource 控制項顯示資料

以下練習使用 SqlDataSource 控制件連接到北風資料庫。 它假定您可以訪問 SQL Server 2000 實例上的北風資料庫。

1. 建立新的 ASP.NET 網站。
2. 添加新的 Web.config 檔案。

    1. 右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。
    2. 從樣本清單中選擇 Web 設定檔,然後單擊" 添加"
3. 編輯&lt;連接字串&gt;部份,如下所示: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 切換到代碼檢視,並將連接String 屬性和 SelectCommand 屬性&lt;新增到 asp:SqlDataSource&gt;控制件,如下所示: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 從"設計"視圖中,添加新的 GridView 控件。
6. 從 GridView 工作選單中的「選擇資料源」下拉清單,選擇 SqlDataSource1。
7. 右鍵按一下 Default.aspx,然後從菜單中選擇「在瀏覽器中查看」。 當提示保存時,單擊"是"。
8. GridView 顯示"產品"表中的數據。

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>練習 2 - 使用 SqlDataSource 控制件編輯資料

下面的練習演示如何使用聲明性語法對下拉清單控件進行數據綁定,並允許您編輯下拉清單控件中顯示的數據。

1. 在"設計"檢視中,從 Default.aspx 中刪除 GridView 控件。 

    **重要提示**:將 SqlDataSource 控制件保留在頁面上。
2. 將下拉清單控制件添加到 Default.aspx。
3. 切換到源視圖。
4. 將 DataSourceId、資料文字欄位和 DataValueField&lt;屬性加入 asp:下拉&gt;清單控制項,如下所示: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. 保存預設.aspx 並在瀏覽器中查看它。 請注意,下拉清單包含來自北風資料庫的所有產品。
6. 關閉瀏覽器。
7. 在 Default.aspx 的來源檢視中,在下拉清單控制元件下方添加新的 TextBox 控制件。 將 TextBox 的 ID 屬性更改為 txtProduct 名稱。
8. 在「文字框」控件下,添加新的「按鈕」控制件。 將按鈕的 ID 屬性更改為 btnUpdate,將文本屬性更改為 **「更新產品名稱**」 。。
9. 在 Default.aspx 的源檢視中,向 SqlDataSource 標籤新增 UpdateCommand 屬性和兩個新的 Update 參數,如下所示: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 請注意,此代碼中添加了兩個更新參數(產品名稱和產品ID)。 這些參數映射到 txtProduct 名稱文字框的文本屬性和 ddlProducts 下拉清單的「選定值」屬性。
10. 切換到"設計"檢視並按兩下"按鈕"控制項以添加事件處理程式。
11. 將以下代碼加入 btnUpdate\_按一個程式碼: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. 右鍵按一下 Default.aspx 並選擇在瀏覽器中查看它。 當提示保存所有更改時,按一下「是」。。
13. ASP.NET 2.0 部分類允許在運行時進行編譯。 無需構建應用程式,以便看到代碼更改生效。
14. 從下拉清單中選擇產品。
15. 在 TextBox 中輸入所選產品的新名稱,然後單擊"更新"按鈕。
16. 產品名稱在資料庫中更新。

## <a name="exercise-3-using-the-objectdatasource-control"></a>練習 3 使用物件資料來源控制項

本練習將演示如何使用ObjectDataSource控制件和來源物件與Northwind資料庫進行互動。

1. 右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。
2. 在範本清單中選擇"Web 窗體"。 將名稱更改為物件.aspx,然後單擊"添加"。
3. 右鍵單擊解決方案資源管理器中的專案,然後單擊"添加新專案"。
4. 在樣本清單中選擇類。 將類的名稱更改為NorthwindData.cs,然後單擊"添加"。
5. 當提示將類添加到應用\_代碼資料夾時,按一下"是"
6. 將以下代碼加入NorthwindData.cs檔: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 將以下代碼加入物件的「原始程式」檢視. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 保存所有文件和流覽物件.aspx。
9. 通過詳細資訊、編輯員工、添加員工和刪除員工與介面進行互動。
