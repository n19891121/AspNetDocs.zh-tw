---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的屬性路由 |微軟文件
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: bb68fe8e6769619029a3fa039d6f0d6f3303afbe
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675390"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的屬性路由

由[邁克·瓦森](https://github.com/MikeWasson)

*路由*是 Web API 將 URI 與操作匹配的方式。 Web API 2 支援一種稱為*屬性路由*的新型路由。 顧名思義,屬性路由使用屬性來定義路由。 屬性路由使您能夠對 Web API 中的 URI 進行更多控制。 例如,您可以輕鬆地創建描述資源層次結構的 URI。

早期路由樣式(稱為基於約定的路由)仍完全支援。 事實上,您可以將這兩種技術合併到同一專案中。

本主題演示如何啟用屬性路由,並介紹屬性路由的各種選項。 有關使用屬性路由的端到端教程,請參閱[在 Web API 2 中使用屬性路由創建 REST API。](create-a-rest-api-with-attribute-routing.md)

## <a name="prerequisites"></a>Prerequisites

[視覺工作室 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區版、專業版或企業版

或者,使用 NuGet 包管理器安裝必要的包。 從 Visual Studio 中的 **「工具**」功能表中,選擇**NuGet 套件管理器**,然後選擇 **「包管理器控制台**」。 在套件管理員主控台視窗中輸入以下指令:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>為什麼選擇屬性路由?

Web API 的第一個版本使用了*基於約定的*路由。 在這種類型的路由中,定義一個或多個路由範本,這些範本基本上是參數化字串。 當框架收到請求時,它將URI與路由範本匹配。 有關基於約定的路由的詳細資訊,請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

基於約定的路由的一個優點是範本在一個位置定義,並且路由規則在所有控制器之間一致應用。 遺憾的是,基於約定的路由很難支援 RESTful API 中常見的某些 URI 模式。 例如,資源通常包含子資源:客戶有訂單,電影有演員,書籍有作者,等等。 建立反映這些關係的 URI 是很自然的:

`/customers/1/orders`

這種類型的URI很難使用基於約定的路由創建。 儘管可以做到這一點,但如果您有許多控制器或資源類型,則結果不會很好地擴展。

使用屬性路由,為此URI定義路由非常簡單。 只需向控制器操作新增屬性:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

下面是一些其他模式,屬性路由使容易。

**API 版本控制**

在此示例中,"/api/v1/產品"將路由到與"/api/v2/產品"不同的控制器。

`/api/v1/products`
`/api/v2/products`

**重載 URI 段**

在此示例中,「1」是訂單號,但「掛起」映射到集合。

`/orders/1`
`/orders/pending`

**多種參數類型**

在此示例中,"1"是訂單號,但"2013/06/16"指定日期。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>開啟屬性路由

要啟用屬性路由,請在配置期間調用**MapHttpAttributeRoutes。** 此擴充方法在**System.Web.http.HTTP:設定擴充**套件中定義。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

屬性路由可以與[基於約定的](routing-in-aspnet-web-api.md)路由組合使用。 要定義基於約定的路由,請調用**MapHTTPRoute**方法。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

有關設定 Web API 的詳細資訊,請參閱[設定 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意:從 Web API 1 移轉

在 Web API 2 之前,Web API 專案樣本產生了如下所示的代碼:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

如果啟用了屬性路由,則此代碼將引發異常。 如果將現有 Web API 專案升級為使用屬性路由,請確保將此設定代碼更新為以下內容:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 有關詳細資訊,請參閱[使用託管ASP.NET配置 Web API。](../advanced/configuring-aspnet-web-api.md#webhost)

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>新增路由屬性

下面是使用屬性定義的路由的範例:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

字串&quot;客戶/[客戶 Id]/&quot;訂單 是路由的 URI 範本。 Web API 嘗試將請求 URI 與範本匹配。 在此示例中,"客戶"和"訂單"是文本段,"[客戶Id]"是一個變數參數。 以下 URI 將符合此樣本:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

您可以使用[約束](#constraints)來限制匹配,本主題稍後將介紹。

請注意,&quot;製程路線樣本中的&quot;{customerId} 參數與 方法中的*customerId*參數的名稱匹配。 當 Web API 呼叫控制器操作時,它嘗試綁定路由參數。 例如,如果 URI`http://example.com/customers/1/orders`是 ,Web API 會嘗試在操作中將值「1」綁定到*customerId*參數。

URI 樣本可以具有多個參數:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

沒有任何路由屬性的控制器方法都使用基於約定的路由。 這樣,可以將兩種類型的路由合併到同一專案中。

## <a name="http-methods"></a>HTTP 方法

Web API 還根據請求的 HTTP 方法(GET、POST 等)選擇操作。 默認情況下,Web API 查找與控制器方法名稱開頭不區分大小寫的匹配。 例如,名為的`PutCustomers`控制器方法與 HTTP PUT 請求匹配。

您可以通過使用以下任何屬性修飾方法來重寫此約定:

- **[ HttpDelete]**
- **[HttpGet]**
- **[HTTPHead]**
- **【 HttpOptions]**
- **[HTTPPatch]**
- **[ HTTPPost]**
- **[HttpPut]**

下面的範例將 CreateBook 方法映射到 HTTP POST 請求。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

對於所有其他 HTTP 方法(包括非標準方法),請使用**AcceptVerbs**屬性,該屬性採用 HTTP 方法的清單。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>路由前置碼

通常,控制器中的路由都以相同的首碼開頭。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

您可以使用 **[RoutePrefix]** 屬性為整個控制器設定公共前置前置字串:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

在方法屬性上使用波浪線 (*) 來覆蓋路由首碼:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

路由前置字串可以包含參數:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>路由約束

通過路由約束,您可以限制路由範本中的參數的匹配方式。 一般語法是&quot;[參數:&quot;約束 ] 。 例如：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

此處,僅當URI的ID&quot;&quot;段是整數時,才會選擇第一個路由。 否則,將選擇第二個路由。

下表列出了支援的約束。

| 條件約束 | 描述 | 範例 |
| --- | --- | --- |
| alpha | 符合大寫或小寫拉丁字母字元(a-z,A-Z) | [x:阿爾法] |
| bool | 匹配布爾值。 | {x:布爾] |
| Datetime | 匹配**日期時間**值。 | [x:日期時間] |
| decimal | 匹配十進位值。 | [x:十進位] |
| double | 匹配64位浮點值。 | [x:雙] |
| FLOAT | 匹配 32 位浮點值。 | [x:浮動] |
| guid | 匹配 GUID 值。 | {x:吉德] |
| int | 匹配 32 位整數值。 | {x:int} |
| 長度 | 將字串與指定長度或指定長度範圍內的字串匹配。 | [x:長度(6)][x:長度(1,20)] |
| long | 匹配64位整數值。 | [x:長] |
| max | 匹配具有最大值的整數。 | {x:最大(10)] |
| 最大長度 | 匹配具有最大長度的字串。 | {x:最大長度(10)] |
| Min | 匹配具有最小值的整數。 | {x:min(10)] |
| 最小長度 | 匹配長度最小的字串。 | {x:最小長度(10)] |
| range | 匹配值範圍內的整數。 | [x:範圍(10,50)] |
| RegEx | 匹配正則表達式。 | {x:regex(\d{3}-d{3}-\d{4}$)] |

請注意,某些約束(如&quot;最小&quot;值)在括弧中採用參數。 您可以將多個約束應用於參數,由冒號分隔。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>自訂路由限制式

您可以通過實現**IHTTPRoute 約束**介面來創建自訂路由約束。 例如,以下約束將參數限制為非零整數值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

以下代碼展示如何註冊約束:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

現在,您可以在路由中應用約束:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

您還可以通過實現**IInline 約束解析器**介面來替換整個**預設內聯約束解析器**類。 這樣做將替換所有內置約束,除非您的**IInline 約束解析器**的實現專門添加它們。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>選擇的 URI 參數與預設值

您可以通過向路由參數添加問號來使 URI 參數成為可選參數。 如果路由參數是可選的,則必須為方法參數定義預設值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

在此範例中,`/api/books/locale/1033``/api/books/locale`並傳回相同的資源。

或者,您可以在工藝路線範本中指定預設值,如下所示:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

這幾乎與前一個示例相同,但在應用預設值時,行為有細微差異。

- 在第一個示例("{lcid:int?}")中,默認值 1033 直接分配給方法參數,因此參數將具有此精確值。
- 在第二個示例("{lcid:int=1033})中,"1033"的默認值通過模型綁定過程。 預設模型綁定器將「1033」轉換為數值 1033。 但是,您可以插入自定義模型活頁夾,這可能執行不同操作。

(在大多數情況下,除非您管道中有自定義模型綁定器,否則這兩個窗體將等效。

<a id="route-names"></a>
## <a name="route-names"></a>路由名稱

在 Web API 中,每個路由都有一個名稱。 路由名稱可用於生成連結,因此您可以在 HTTP 回應中包含連結。

要指定路由名稱,請在屬性上設定**Name**屬性。 下面的範例示範如何設置路由名稱,以及生成連結時如何使用路由名稱。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>路線訂單

當框架嘗試將URI與路由匹配時,它會按特定順序評估路由。 要指定訂單,請在工藝路線屬性上設置**Order**屬性。 首先計算較低的值。 默認訂單值為零。

以下是確定總排序的方式:

1. 比較工藝路線屬性的**Order**屬性。
2. 查看工藝路線範本中的每個 URI 段。 對於每個段,順序如下:

    1. 欄位。
    2. 具有約束的路由參數。
    3. 路由參數沒有約束。
    4. 具有約束的通配符參數段。
    5. 通配符參數段沒有約束。
3. 在連接的情況下,路由由路由範本的區分大小寫序字串比較[(OrdinalIgnoreCase)](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)排序。

範例如下。 假設您定義以下控制器:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

這些路線按如下方式排序。

1. 訂單/詳細資訊
2. 訂單/{id}
3. 訂單/[客戶名稱]
4. 訂單/*\*日期*
5. 訂單/待定

請注意,"詳細資訊"是文本段,出現在"{id}"之前,但"掛起"顯示最後,因為**Order**屬性為 1。 (此示例假定沒有名為"詳細資訊"或"掛起"的客戶。 通常,盡量避免不明確的路線。 在此示例中,更好的`GetByCustomer`路由範本是"客戶/[客戶名稱]"
