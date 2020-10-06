---
uid: web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
title: 支援 ASP.NET Web API 2-ASP.NET 4.x 中的 OData 查詢選項
author: MikeWasson
description: 使用程式碼範例的總覽會顯示 ASP.NET Web API 2 中適用于 ASP.NET 4.x 的支援 OData 查詢選項。
ms.author: riande
ms.date: 02/04/2013
ms.custom: seoapril2019
ms.assetid: 50e6e62b-e72e-4a29-8293-4b67377bd21f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/supporting-odata-query-options
msc.type: authoredcontent
ms.openlocfilehash: 96820fab7ac89885058962f44ded86cb0184ee97
ms.sourcegitcommit: 4ed0b65ae32d9f35e42ee6296b877747e063df4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "86188609"
---
# <a name="supporting-odata-query-options-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中支援 OData 查詢選項

由 [Mike Wasson](https://github.com/MikeWasson)

下列程式碼範例會示範 ASP.NET 4.x 的 ASP.NET Web API 2 中支援的 OData 查詢選項。 

OData 定義可用於修改 OData 查詢的參數。 用戶端會在要求 URI 的查詢字串中傳送這些參數。 例如，若要排序結果，用戶端會使用 $orderby 參數：

`http://localhost/Products?$orderby=Name`

OData 規格會呼叫這些參數 *查詢選項*。 您可以針對專案中的任何 Web API 控制器啟用 OData 查詢選項 &#8212; 控制器不需要是 OData 端點。 這可讓您輕鬆地將篩選和排序等功能新增至任何 Web API 應用程式。

啟用查詢選項之前，請閱讀《 [OData 安全性指南](odata-security-guidance.md)」主題。

- [啟用 OData 查詢選項](#enable)
- [範例查詢](#examples)
- [伺服器導向的分頁](#server-paging)
- [限制查詢選項](#limiting_query_options)
- [直接叫用查詢選項](#ODataQueryOptions)
- [查詢驗證](#query-validation)

<a id="enable"></a>
## <a name="enabling-odata-query-options"></a>啟用 OData 查詢選項

Web API 支援下列 OData 查詢選項：

| 選項 | 說明 |
| --- | --- |
| $expand | 展開內嵌相關的實體。 |
| $filter | 根據布林值條件篩選結果。 |
| $inlinecount | 告訴伺服器在回應中包含相符實體的總計數。  (適用于伺服器端分頁。 )  |
| $orderby | 排序結果。 |
| $select | 選取要包含在回應中的屬性。 |
| $skip | 略過前 n 個結果。 |
| $top | 只傳回結果的前 n 個。 |

若要使用 OData 查詢選項，您必須明確加以啟用。 您可以針對整個應用程式全域啟用它們，或針對特定控制器或特定動作來啟用它們。

若要全域啟用 OData 查詢選項，請在啟動時呼叫**HttpConfiguration**類別上的**EnableQuerySupport** ：

[!code-csharp[Main](supporting-odata-query-options/samples/sample1.cs)]

**EnableQuerySupport**方法會針對傳回**IQueryable**型別的任何控制器動作，全域啟用查詢選項。 如果您不想要針對整個應用程式啟用查詢選項，可以將 **[可查詢]** 屬性新增至動作方法，以針對特定控制器動作啟用它們。

[!code-csharp[Main](supporting-odata-query-options/samples/sample2.cs)]

<a id="examples"></a>
## <a name="example-queries"></a>查詢範例

本節說明可以使用 OData 查詢選項的查詢類型。 如需查詢選項的特定詳細資料，請參閱 OData 檔，網址 [www.odata.org](http://www.odata.org/)。

如需 $expand 和 $select 的詳細資訊，請參閱 [$Value OData 中的使用 $select、$expand 和 ASP.NET Web API](using-select-expand-and-value.md)。

**用戶端驅動分頁**

針對大型實體集，用戶端可能會想要限制結果數目。 例如，用戶端可能會一次顯示10個專案，並使用 [下一步] 連結來取得下一個結果頁。 若要這樣做，用戶端會使用 $top 並 $skip 選項。

`http://localhost/Products?$top=10&$skip=20`

$Top 選項會提供要傳回的最大專案數，而 $skip 選項會提供要略過的專案數。 先前的範例會提取21到30的專案。

**篩選**

$Filter 選項可讓用戶端套用布林運算式來篩選結果。 篩選運算式相當強大;它們包括邏輯和算術運算子、字串函數和日期函數。

| 傳回類別等於「玩具」的所有產品。 | `http://localhost/Products?$filter=Category` eq ' 玩具 ' |
| --- | --- |
| 傳回價格小於10的所有產品。 | `http://localhost/Products?$filter=Price` lt 10 |
| 邏輯運算子：傳回價格 >= 5 且價格 <= 15 的所有產品。 | `http://localhost/Products?$filter=Price` ge 5 和價格 le 15 |
| 字串函數：傳回名稱中有 "zz" 的所有產品。 | `http://localhost/Products?$filter=substringof('zz',Name)` |
| 日期函數：傳回 ReleaseDate 晚于2005的所有產品。 | `http://localhost/Products?$filter=year(ReleaseDate)` gt 2005 |

**排序**

若要排序結果，請使用 $orderby 篩選準則。

| 依價格排序。 | `http://localhost/Products?$orderby=Price` |
| --- | --- |
| 依價格以遞減順序排序， (最高至最低) 。 | `http://localhost/Products?$orderby=Price desc` |
| 依類別排序，然後依類別中的遞減順序排序。 | `http://localhost/odata/Products?$orderby=Category,Price desc` |

<a id="server-paging"></a>
## <a name="server-driven-paging"></a>伺服器導向的分頁

如果您的資料庫包含數百萬筆記錄，您就不會想要在一個承載中全部傳送。 為了避免這種情況，伺服器可限制在單一回應中傳送的專案數目。 若要啟用伺服器分頁，請在可**查詢**的屬性中設定**PageSize**屬性。 值是要傳回的最大專案數。

[!code-csharp[Main](supporting-odata-query-options/samples/sample3.cs)]

如果您的控制器傳回 OData 格式，回應主體會包含下一個資料頁面的連結：

[!code-json[Main](supporting-odata-query-options/samples/sample4.json?highlight=8)]

用戶端可以使用此連結來提取下一個頁面。 若要瞭解結果集中的專案總數，用戶端可以使用 "allpages 提出要求" 值來設定 $inlinecount 查詢選項。

`http://localhost/Products?$inlinecount=allpages`

值 "allpages 提出要求" 會告訴伺服器在回應中包含總計計數：

[!code-json[Main](supporting-odata-query-options/samples/sample5.json?highlight=3)]

> [!NOTE]
> 下一頁連結和內嵌計數都需要 OData 格式。 原因是 OData 在回應主體中定義特殊欄位以保存連結和計數。

針對非 OData 格式，您仍然可以支援下一頁連結和內嵌計數，方法是將查詢結果包裝在**PageResult &lt; T &gt; **物件中。 不過，它需要更多程式碼。 範例如下：

[!code-csharp[Main](supporting-odata-query-options/samples/sample6.cs)]

以下是範例 JSON 回應：

[!code-json[Main](supporting-odata-query-options/samples/sample7.json)]

<a id="limiting_query_options"></a>
## <a name="limiting-the-query-options"></a>限制查詢選項

查詢選項讓用戶端對伺服器上執行的查詢有很大的控制權。 在某些情況下，您可能會想要限制安全性或效能原因的可用選項。 **[可查詢]** 屬性具有這個的一些內建屬性。 以下是一些範例。

只允許 $skip 和 $top 支援分頁和其他任何專案：

[!code-csharp[Main](supporting-odata-query-options/samples/sample8.cs)]

只允許某些屬性進行排序，以防止針對資料庫中未編制索引的屬性進行排序：

[!code-csharp[Main](supporting-odata-query-options/samples/sample9.cs)]

允許 "eq" 邏輯函式，但不允許其他邏輯函數：

[!code-csharp[Main](supporting-odata-query-options/samples/sample10.cs)]

不允許任何算術運算子：

[!code-csharp[Main](supporting-odata-query-options/samples/sample11.cs)]

您可以藉由建立 **QueryableAttribute** 實例並將其傳遞至 **EnableQuerySupport** 函式，來限制全域選項：

[!code-csharp[Main](supporting-odata-query-options/samples/sample12.cs)]

<a id="ODataQueryOptions"></a>
## <a name="invoking-query-options-directly"></a>直接叫用查詢選項

您可以直接在控制器中叫用查詢選項，而不使用 **[可查詢]** 屬性。 若要這樣做，請將 **ODataQueryOptions** 參數加入至控制器方法。 在此情況下，您不需要 **[可查詢]** 屬性。

[!code-csharp[Main](supporting-odata-query-options/samples/sample13.cs)]

Web API 會在 **ODataQueryOptions** 中填入 URI 查詢字串。 若要套用查詢，請將 **IQueryable** 傳遞給 **ApplyTo** 方法。 方法會傳回另一個 **IQueryable**。

針對先進的案例，如果您沒有 **IQueryable** 查詢提供者，您可以檢查 **ODataQueryOptions** 並將查詢選項轉譯為另一個表單。  (例如，請參閱 RaghuRam Nadiminti 的 blog 文章 [將 OData 查詢轉譯為 HQL](https://blogs.msdn.com/b/webdev/archive/2013/02/25/translating-odata-queries-to-hql.aspx)，其中也包含 [範例](http://aspnet.codeplex.com/SourceControl/changeset/view/75a56ec99968#Samples/WebApi/NHibernateQueryableSample/Readme.txt)。 ) 

<a id="query-validation"></a>
## <a name="query-validation"></a>查詢驗證

**[可查詢]** 屬性會在執行查詢之前進行驗證。 驗證步驟是在 **QueryableAttribute. ValidateQuery** 方法中執行。 您也可以自訂驗證流程。

另請參閱 [OData 安全性指引](odata-security-guidance.md)。

首先，覆寫在 **web.config** 命名空間中定義的其中一個驗證程式類別。 例如，下列驗證程式類別會停用 $orderby 選項的 ' desc ' 選項。

[!code-csharp[Main](supporting-odata-query-options/samples/sample14.cs)]

子類別化 **[可查詢]** 屬性以覆寫 **ValidateQuery** 方法。

[!code-csharp[Main](supporting-odata-query-options/samples/sample15.cs)]

然後，將您的自訂屬性設定為全域或每個控制器：

[!code-csharp[Main](supporting-odata-query-options/samples/sample16.cs)]

如果您直接使用 **ODataQueryOptions** ，請在選項上設定驗證程式：

[!code-csharp[Main](supporting-odata-query-options/samples/sample17.cs)]
