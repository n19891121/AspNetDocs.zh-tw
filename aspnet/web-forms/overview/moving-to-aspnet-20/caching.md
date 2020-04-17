---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 快取 |微軟文件
author: rick-anderson
description: 對緩存的理解對於性能良好的ASP.NET應用程式非常重要。 ASP.NET 1.x 提供了三種不同的緩存選項;輸出快取,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: a199a9c0352dfb054e8d4e5e67652db9bd38851c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542933"
---
# <a name="caching"></a>Caching

由[微軟](https://github.com/microsoft)

> 對緩存的理解對於性能良好的ASP.NET應用程式非常重要。 ASP.NET 1.x 提供了三種不同的緩存選項;輸出緩存、片段快取和快取 API。

對緩存的理解對於性能良好的ASP.NET應用程式非常重要。 ASP.NET 1.x 提供了三種不同的緩存選項;輸出緩存、片段快取和快取 API。 ASP.NET 2.0 提供了所有三種方法,但它增加了一些重要的附加功能。 有幾個新的緩存依賴項,開發人員現在也可以選擇創建自定義緩存依賴項。 緩存的配置在ASP.NET 2.0 中也得到了顯著改善。

## <a name="new-features"></a>新功能

## <a name="cache-profiles"></a>快取設定檔

快取設定檔允許開發人員定義特定的快取設定,然後可以應用於各個頁面。 例如,如果您有一些頁面應在 12 小時後從快取中過期,則可以輕鬆地創建可應用於這些頁面的緩存配置檔。 要新增新的快取設定檔,請使用設定檔中的&lt;輸出快取&gt;設定部分。 例如,下面是一個稱為*兩天的*快取配置檔的配置,該配置檔配置的快取持續時間為 12 小時。

[!code-xml[Main](caching/samples/sample1.xml)]

要將此快取設定檔套用於特定頁面,請使用 @ OutputCache 指令的 CacheProfile 屬性,如下所示:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>自訂快取相依項

ASP.NET 1.x 開發人員大聲疾呼自定義緩存依賴項。 在ASP.NET 1.x 中,CacheDependency 類被密封,阻止開發人員從中派生自己的類。 在 ASP.NET 2.0 中,該限制被刪除,開發人員可以自由地開發自己的自定義緩存依賴項。 CacheDependency 類允許基於檔、目錄或緩存鍵創建自定義緩存依賴項。

例如,下面的代碼基於位於 Web 應用程式根目錄的名為 stuff.xml 的檔案建立新的自訂緩存依賴項:

[!code-csharp[Main](caching/samples/sample3.cs)]

在這種情況下,當 stuff.xml 檔發生更改時,快取的項將失效。

還可以使用緩存鍵創建自定義緩存依賴項。 使用此方法,刪除快取金鑰將使快取的資料無效。 下列範例會加以說明：

[!code-csharp[Main](caching/samples/sample4.cs)]

要使上面插入的項無效,只需刪除插入到緩存中的項,即可充當緩存鍵。

[!code-csharp[Main](caching/samples/sample5.cs)]

請注意,充當緩存鍵的項的鍵必須與添加到緩存鍵陣列的值相同。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>基於輪詢的 SQL 快取依賴項(也稱為基於表的依賴項)

SQL Server 7 和 2000 使用基於輪詢的模型進行 SQL 緩存依賴項。 基於輪詢的模型使用資料庫表上的觸發器,該觸發器在表中的數據更改時觸發。 該觸發器更新通知表中ASP.NET定期檢查的**更改Id**欄位。 如果已更新**changeId**欄位,ASP.NET知道數據已更改,並且會使緩存的數據無效。

> [!NOTE]
> SQL Server 2005 也可以使用基於輪詢的模型,但由於基於輪詢的模型不是最有效的模型,因此最好在 SQL Server 2005 中使用基於查詢的模型(稍後討論)。

為了使使用基於輪詢的模型的 SQL 快取依賴項正常工作,表必須啟用通知。 這可以通過 SqlCache 獨立管理類或使用\_aspnet regsql.exe 實用程式以程式設計方式完成。

以下命令列在位於 SQL Server 實例上的 Northwind 資料庫中註冊產品表,該實例名為*dbase,* 用於 SQL 緩存依賴項。

[!code-console[Main](caching/samples/sample6.cmd)]

以下是上述命令中使用的命令行開關的說明:

| **命令列開關** | **目的** |
| --- | --- |
| -S *server* | 指定伺服器名稱。 |
| -ed | 指定應為 SQL 快取依賴項啟用資料庫。 |
| -d*\_資料庫名稱* | 指定應為 SQL 快取依賴項啟用的資料庫名稱。 |
| -E | 指定 aspnet\_regsql 連接到資料庫時應使用 Windows 身份驗證。 |
| -et | 指定我們正在為 SQL 快取依賴項啟用資料庫表。 |
| -t*\_表名稱* | 指定資料庫表的名稱,以便為 SQL 快取依賴項啟用。 |

> [!NOTE]
> 還有其他可用於 aspnet\_regsql.exe 的交換機。 對於完整清單,執行 aspnet\_regsql.exe -? 從命令行。

執行此指令時,對 SQL Server 資料庫進行了以下變更:

- 將新增**AspNet\_SqlCacheTables 用於變更通知表**。 此表包含資料庫中已為其啟用 SQL 快取依賴項的每個表的一行。
- 在資料庫內部建立以下儲存程序:

| 阿斯普內\_SqlCache 儲存過程 | 查詢 AspNet\_SqlCacheTablesForChange 通知表,並傳回為 SQL 快取依賴項啟用的所有表以及每個表的 changeId 值。 此存儲的 proc 用於輪詢以確定數據是否已更改。 |
| --- | --- |
| AspNet\_SqlCache 查詢註冊表儲存程序 | 通過查詢 AspNet\_SqlCacheTablesForChange 通知表來返回為 SQL 快取依賴項啟用的所有表,並返回為 SQL 快取依賴項啟用的所有表。 |
| 阿斯普內\_SqlCache 註冊表儲存過程 | 通過在通知表中添加必要的條目並添加觸發器來註冊 SQL 緩存依賴項的表。 |
| 阿斯普內\_SqlCacheUn 寄存器表記憶體 | 通過刪除通知表中的條目並刪除觸發器,取消註冊 SQL 快取依賴項的表。 |
| 阿斯普內\_SqlCache 更新變更儲存過程 | 通過增加已更改表的 changeId 來更新通知表。 ASP.NET使用此值來確定數據是否已更改。 如下所述,此存儲的 proc 由啟用表時創建的觸發器執行。 |

- 為表建立 SQL Server 觸發器**_,\_稱為表格名稱_\_AspNet\_\_SqlCache 通知 觸發器**。 當在表上執行插入、更新\_或刪除時,此觸發器將執行 AspNet SqlCache 更新更改儲存過程。
- SQL Server 角色稱為**\_\_aspnet 更改通知接收通知僅訪問**已添加到資料庫中。

**aspnet\_更改\_通知 僅接收通知訪問**SQL 伺服器角色具有\_對 AspNet SqlCache 投票儲存過程的 EXEC 許可權。 為了使輪詢模型正常工作,您必須將行程帳戶添加到 aspnet\_更改\_通知 僅接收通知訪問角色。 aspnet\_regsql.exe 工具不會為您執行此操作。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>設定基於輪詢的 SQL 快取相依項

配置基於輪詢的 SQL 緩存依賴項需要幾個步驟。 第一步是啟用資料庫和表,如上所述。 完成此步驟后,配置的其餘部分如下所示:

- 配置ASP.NET配置檔。
- 設定 SqlCache 相依性

### <a name="configuring-the-aspnet-configuration-file"></a>設定ASP.NET設定檔

除了新增上一個模組中討論的連接字串外&lt;, 您必須使用&gt;&lt;sqlCacheDependency&gt;元素設定緩存元素,如下所示:

[!code-xml[Main](caching/samples/sample7.xml)]

此設定啟用對*pubs*資料庫的 SQL 快取依賴項。 請注意,sqlCache 依賴&lt;&gt;元素 中的 pollTime 屬性預設為 60000 毫秒或 1 分鐘。 (此值不能小於 500 毫秒。在此範例中,add&lt;&gt;元素添加新資料庫並覆蓋輪詢Time,將其設置為9000000毫秒。

#### <a name="configuring-the-sqlcachedependency"></a>設定 SqlCache 相依性

下一步是配置 SqlCache 依賴性。 此目的的最簡單方法是在 @ Outcache 指令中指定 SqlDependency 屬性的值,如下所示:

[!code-aspx[Main](caching/samples/sample8.aspx)]

在上述輸出緩存指令中,為*pubs*資料庫中*的作者*表配置了 SQL 快取依賴項。 可以通過將多個依賴項與分號分隔來配置,如下所示:

[!code-aspx[Main](caching/samples/sample9.aspx)]

配置 SqlCache 依賴性的另一種方法是在程式設計方式中配置。 以下代碼在*pubs*資料庫中創建對*作者*表的新 SQL 快取依賴項。

[!code-csharp[Main](caching/samples/sample10.cs)]

以程式設計方式定義 SQL 緩存依賴項的好處之一是可以處理可能發生的任何異常。 例如,如果嘗試為尚未為通知啟用的資料庫定義 SQL 快取依賴項,則會引發**資料庫未啟用通知異常異常**。 在這種情況下,您可以嘗試通過調用**SqlCache 獨立Admin.enable通知**方法並傳遞資料庫名稱來啟用資料庫的通知。

同樣,如果嘗試為尚未為通知啟用的表定義 SQL 快取依賴項,將引發**表未啟用For通知異常**。 然後,您可以調用**SqlCache 獨立Admin.啟用TableFor通知**方法,傳遞資料庫名稱和表名稱。

以下代碼示例說明瞭在配置 SQL 快取依賴項時如何正確配置異常處理。

[!code-csharp[Main](caching/samples/sample11.cs)]

更多資訊:[https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>查詢的 SQL 快取相依項(僅限 SQL Server 2005)

當 SQL Server 2005 用於 SQL 緩存依賴項時,不需要基於輪詢的模型。 當與 SQL Server 2005 一起使用時,SQL 快取依賴項直接透過 SQL 連接到 SQL Server 實例(無需進一步配置)使用 SQL Server 2005 查詢通知。

啟用基於查詢的通知的最簡單方法是透過將資料源物件的**SqlCacheDependency 屬性**設定為**指令通知**並將**EnableCaching**屬性設定為**true**來聲明性地執行此操作。 使用此方法,不需要任何代碼。 如果針對數據源執行的命令的結果發生更改,它將使緩存數據失效。

以下範例為 SQL 快取相依項設定資料來源控制項:

[!code-aspx[Main](caching/samples/sample12.aspx)]

在這種情況下,如果**SelectCommand**中指定的查詢返回的結果與最初的結果不同,則緩存的結果將失效。

還可以透過您@**OutputCache**指令的**SqlIis**屬性設定為**指令通知**,指定為 SQL 快取相依項啟用所有資料來源。 下面的示例說明瞭這一點。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> 有關 SQL Server 2005 中的查詢通知的詳細資訊,請參閱 SQL 伺服器連線書籍。

配置基於查詢的 SQL 快取依賴項的另一種方法是使用 SqlCache 依賴類以程式設計方式執行此操作。 以下代碼示例說明瞭如何實現此目的。

[!code-csharp[Main](caching/samples/sample14.cs)]

更多資訊:[https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>快取後取代

緩存頁面可以顯著提高 Web 應用程式的性能。 但是,在某些情況下,您需要緩存大部分頁面,並且頁面中的某些片段是動態的。 例如,如果創建的新聞報導頁面在設定的時間段內是完全靜態的,則可以將整個頁面設置為緩存。 如果要包含在每個頁面請求中更改的旋轉廣告橫幅,則包含廣告的頁面部分必須是動態的。 為了允許您快取頁面但動態替換某些內容,可以使用ASP.NET緩存後替換。 使用緩存後替換時,整個頁面的輸出將緩存,並帶有標記為免於緩存的特定部件。 在廣告橫幅範例中,AdRotator 控制項允許您利用緩存後替換,以便為每個使用者和每個頁面刷新動態創建廣告。

有三種方法可以實現緩存後取代:

- 聲明性,使用替換控制項。
- 在程式設計上,使用替換控制項 API。
- 隱式,使用 AdRotator 控制件。

### <a name="substitution-control"></a>替代控制

ASP.NET替換控制項指定以動態創建而不是快取的快取頁面的一部分。 將替換控制項放置在您希望顯示動態內容的頁面上的位置。 在執行時,替換控制器呼叫使用 MethodName 屬性指定的方法。 該方法必須返回一個字串,然後替換替換控件的內容。 該方法必須是包含頁面或使用者控制控制件上的靜態方法。 使用替換控制項會導致客戶端可緩存性更改為伺服器可緩存性,因此頁面不會緩存在用戶端上。 這可確保將來對頁面的請求再次調用 方法以生成動態內容。

### <a name="substitution-api"></a>取代 API

要以程式設計方式為緩存頁面創建動態內容,可以在頁面代碼中調用[Write替代](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)方法,將其作為參數傳遞方法的名稱。 處理動態內容建立的方法需要單個[HTTPContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)參數並返回字串。 返回字串是在給定位置替換的內容。 呼叫 Write 替代方法而不是聲明性使用替換控制項的優點是,您可以呼叫任意物件的方法,而不是調用 Page 或 UserControl 物件的靜態方法。

呼叫 Write 替代方法會導致用戶端可快取性更改為伺服器可緩存性,因此頁面不會緩存在用戶端上。 這可確保將來對頁面的請求再次調用 方法以生成動態內容。

### <a name="adrotator-control"></a>輔助器控制

AdRotator 伺服器控制檔在內部實現對快取後替換的支援。 如果將 AdRotator 控制件放在頁面上,它將在每個請求上呈現唯一的廣告,而不管父頁是否緩存。 因此,包含 AdRotator 控制件的頁面僅快取伺服器端。

## <a name="controlcachepolicy-class"></a>控制項快取原則類別

ControlCachePolicy 類允許使用使用者控制項對片段緩存進行程式設計控制。 ASP.NET將使用者控制件嵌入[到基本部分緩存控制](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)實例中。 Base部分緩存控制類表示已啟用輸出緩存的使用者控制項。

當您存[取 部分快取控制的](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)[Base 部分快取控制.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)屬性時,您始終會收到有效的 ControlCachePolicy 物件。 但是,如果您訪問[UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) [屬性的使用者控制控制件](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx),則只有在使用者控制件已由 Base 部分緩存控制件包包時,才會收到有效的 ControlCachePolicy 物件。 如果未包裝,則屬性返回的 ControlCachePolicy 物件將引發異常,當您嘗試操作它時,因為它沒有關聯的 BasePartial CachingControl。 要確定 UserControl 實體是否支援快取而不生成異常,請檢查[「支援快取」](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)屬性。

使用 ControlCachePolicy 類是啟用輸出緩存的幾種方法之一。 下面的清單描述了可用於啟用輸出快取的方法:

- 使用[# 輸出快取](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令在宣告性方案中啟用輸出快取。
- 使用[「部分快取屬性」屬性](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)為代碼背後的檔案中的使用者控制件啟用緩存。
- 使用 ControlCachePolicy 類指定在程式設計方案中的緩存設定,其中您正在使用以前的方法之一使用已啟用緩存並使用[System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)方法動態載入的 BasePartialCacheControl 實例。

只能在控制生命週期的 Init 和預算式階段之間成功操作 ControlCachePolicy 實例。 如果在 PreRender 階段後修改 ControlCachePolicy 物件,ASP.NET將引發異常,因為在呈現控制項後所做的任何更改實際上不會影響緩存設置(在渲染階段緩存控件)。 最後,使用者控件實例(因此其 ControlCachePolicy 物件)僅在實際呈現時才可用於程式設計操作。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>快取設定的&lt;變更 - 快&gt;取元素

ASP.NET 2.0 中緩存配置有幾個更改。 快取&lt;&gt;元素在 ASP.NET 2.0 中是新的,允許您在設定檔中進行更改快取設定。 以下屬性可用。

| **項目** | **說明** |
| --- | --- |
| **快取** | 選擇性項目。 定義全域應用程式緩存設置。 |
| **輸出快取** | 選擇性項目。 指定應用程式範圍的輸出緩存設置。 |
| **outputCacheSettings** | 選擇性項目。 指定可應用於應用程式中的頁面的輸出緩存設置。 |
| **sqlCacheDependency** | 選擇性項目。 設定 ASP.NET 應用程式的 SQL 快取相依性。 |

### <a name="the-ltcachegt-element"></a>快取&lt;&gt;元素

快取&lt;&gt;元素中提供以下屬性:

| **屬性** | **說明** |
| --- | --- |
| **關閉記憶體收集** | 選擇性 **Boolean** 屬性。 獲取或設置一個值,指示計算機處於內存壓力下時發生的緩存記憶體集合是否被禁用。 |
| **停用過期** | 選擇性 **Boolean** 屬性。 獲取或設置指示是否禁用緩存過期的值。 禁用後,緩存的專案不會過期,也不會發生過期緩存項的後台清理。 |
| **私密位元組限制** | 可選**的 Int64**屬性。 在緩存開始刷新過期項目並嘗試回收記憶體之前獲取或設置指示應用程式專用位元組的最大大小的值。 此限制包括快取使用的記憶體以及正在運行的應用程式的正常記憶體開銷。 設置為零表示ASP.NET將使用自己的啟髮式方法來確定何時開始回收記憶體。 |
| **實體記憶體使用限制百分比** | 可選**的 Int32**屬性。 獲取或設置一個值,指示應用程式在開始刷新過期項目並嘗試回收記憶體之前可以使用的計算機物理記憶體的最大百分比。 設置為零表示ASP.NET將使用自己的啟髮式方法來確定何時開始回收記憶體。 |
| **私人位元組投票時間** | 可選**的 TimeSpan**屬性。 獲取或設置一個值,指示應用程式專用位元組記憶體使用方式輪詢之間的時間間隔。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;輸出快取&gt;元素

以下屬性可用於&lt;輸出緩&gt;存 元素。

|       <strong>屬性</strong>        |                                                                                                                                                                                                                                                       <strong>說明</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>開啟輸出快取</strong>    |                                                                                                                                                          選擇性 <strong>Boolean</strong> 屬性。 啟用/禁用頁面輸出緩存。 如果禁用,則無論使用程式設計設置或聲明性設置如何,都不緩存任何頁面。 預設值為<strong>true</strong>。                                                                                                                                                           |
|  <strong>開啟磁碟快取</strong>   |                                                選擇性 <strong>Boolean</strong> 屬性。 啟用/禁用應用程式片段緩存。 如果關閉,則無論使用的[# OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令或快取設定檔如何,都無需快取任何頁面。 包括快取控制標頭,指示上游代理伺服器以及瀏覽器用戶端不應嘗試緩存頁面輸出。 預設值為 <strong>false</strong>。                                                 |
| <strong>送出快取控制標頭</strong> |                                                                                                                                                      選擇性 <strong>Boolean</strong> 屬性。 獲取或設置一個值,指示默認情況下輸出緩存模組是否發送<strong>快存控制:私有</strong>標頭。 預設值為 <strong>false</strong>。                                                                                                                                                      |
|      <strong>省略VaryStar</strong>      | 選擇性 <strong>Boolean</strong> 屬性。 啟用/停用在回應中發送<strong>HTTP「Vary:/\<強<em>>」標頭。使用 false 的預設設定時,</em>\*<strong>將傳送輸出快取頁的「_Vary:「標頭」。發送 Vary 標頭時,它允許根據 Vary 標頭中指定的內容緩存不同的版本。例如<em>,Vary:使用者代理</em>將基於發出請求的使用者代理儲存頁面的不同版本。預設值為 _false</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;輸出快取設定&gt;元素

輸出&lt;快取&gt;設定 元素允許建立快取設定檔,如前面所述。 &lt;輸出快取設定&gt;元素的唯一子元素是用於設定快&lt;取 設定檔&gt;的輸出快取設定檔元素。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCache&gt;相依元素

以下屬性可用於&lt;sqlCache 依賴&gt;元素。

| **屬性** | **說明** |
| --- | --- |
| **開啟** | 必要**的布林屬性**。 指示是否輪詢更改。 |
| **輪詢時間** | 可選**的 Int32**屬性。 設置 SqlCache 依賴項輪詢資料庫表以進行更改的頻率。 此值對應於連續輪詢之間的毫秒數。 不能將其設置為小於 500 毫秒。 默認值為 1 分鐘。 |

### <a name="more-information"></a>相關資訊

關於快取配置,您應該知道一些其他資訊。

- 如果未設定輔助行程專用位元組限制,則快取將使用以下限制之一: 

    - x86 2GB:800MB 或 60% 的物理 RAM,以較低者為準
    - x86 3GB:1800MB 或 60% 的物理 RAM,以較低者為準
    - x64: 1 TB 或 60% 的物理 RAM,以較低者為準
- 如果同時設定輔助行程專用位元組限制&lt;和緩存專用位元組限制&gt;/, 則緩存將使用兩個中的最小值。
- 就像在 1.x 中一樣,我們刪除緩存條目並調用 GC。收集有兩個原因: 

    - 我們非常接近私有位元組限制
    - 可用記憶體接近或小於 10%
- 通過將&lt;快取百分比實體記憶體使用限制/&gt;設定為 100,可以有效地禁用低可用記憶體條件的修剪和緩存。
- 與 1.x 不同,2.0 將掛起修剪並收集上次 GC 時調用。Collect 沒有將私有位元組或託管堆的大小減少超過(緩存)記憶體限制的1%。

## <a name="lab1-custom-cache-dependencies"></a>實驗室 1:自定義緩存依賴項

1. 建立新網站。
2. 添加新的 XML 檔案稱為 cache.xml,並將其保存到 Web 應用程式的根目錄。
3. 在 default.aspx\_的代碼後面加入以下代碼到頁面載入方法: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 將以下內容新增到源檢視中的 default.aspx 的頂部: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 瀏覽預設.aspx。 時間說什麼?
6. 重新整理瀏覽器。 時間說什麼?
7. 開啟 cache.xml 並新增以下代碼: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. 儲存快取.xml。
9. 重新整理您的瀏覽器。 時間說什麼?
10. 解釋為什麼時間更新而不是顯示以前快取的值:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>實驗 2:使用基於輪詢的緩存依賴項

本實驗使用您在上一個模組中創建的專案,該專案允許通過 GridView 和詳細資訊視圖控制件編輯北風資料庫中的數據。

1. 在 Visual Studio 2005 中打開該專案。
2. 根據北風資料庫運行\_aspnet regsql 實用程式,以啟用資料庫和產品表。 使用視覺化工作室指令提示符中的以下指令: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 將以下內容加入到 Web.config 檔案: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 添加新的 Web 表單,稱為 showdata.aspx。
5. 將以下 = 輸出快取指令加入 showdata.aspx 頁面: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 將以下代碼加入 showdata.aspx 的\_頁面 載入: 

    [!code-html[Main](caching/samples/sample21.html)]
7. 添加新的 SqlDataSource 控制項以顯示 data.aspx,並將其配置為使用北風資料庫連接。 按 [下一步]。
8. 選擇"產品名稱"和"產品 ID"複選框,然後單擊"下一步"。
9. 按一下 [完成]。
10. 向 showdata.aspx 頁面添加新的 GridView。
11. 從下拉清單中選擇 SqlDataSource1。
12. 保存和瀏覽顯示數據.aspx。 記下顯示的時間。
