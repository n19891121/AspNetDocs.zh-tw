---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: 從 .NET 用戶端呼叫 OData 服務（C#） |Microsoft Docs
author: MikeWasson
description: 本教學課程說明如何從C#用戶端應用程式呼叫 OData 服務。 教學課程中所使用的軟體版本 Visual Studio 2013 （適用于視覺效果 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600405"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>從 .NET 用戶端呼叫 OData 服務 (C#)

由[Mike Wasson](https://github.com/MikeWasson)

[下載已完成的專案](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 本教學課程說明如何從C#用戶端應用程式呼叫 OData 服務。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) （適用于 Visual Studio 2012）
> - [WCF Data Services 用戶端程式庫](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2。 （範例 OData 服務是使用 Web API 2 來建立的，但用戶端應用程式不會相依于 Web API）。

在本教學課程中，我將逐步解說如何建立呼叫 OData 服務的用戶端應用程式。 OData 服務會公開下列實體：

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

下列文章說明如何在 Web API 中執行 OData 服務。 （不過，您不需要閱讀它們來瞭解此教學課程）。

- [在 Web API 2 中建立 OData 端點](creating-an-odata-endpoint.md)
- [Web API 2 中的 OData 實體關聯](working-with-entity-relations.md)
- [Web API 2 中的 OData 動作](odata-actions.md)

## <a name="generate-the-service-proxy"></a>產生服務 Proxy

第一個步驟是產生服務 proxy。 服務 proxy 是一個 .NET 類別，可定義存取 OData 服務的方法。 Proxy 會將方法呼叫轉譯為 HTTP 要求。

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

首先，在 Visual Studio 中開啟 OData 服務專案。 按下 CTRL + F5，以 IIS Express 在本機執行服務。 請注意本機位址，包括 Visual Studio 指派的通訊埠編號。 當您建立 proxy 時，將需要此位址。

接下來，開啟 Visual Studio 的另一個實例，然後建立主控台應用程式專案。 主控台應用程式將會是我們的 OData 用戶端應用程式。 （您也可以將專案加入至與服務相同的方案）。

> [!NOTE]
> 其餘步驟會參考主控台專案。

在方案總管中，以滑鼠右鍵按一下 [**參考**]，然後選取 [**加入服務參考**]。

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

在 [**加入服務參考**] 對話方塊中，輸入 OData 服務的位址：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

其中*port*是埠號碼。

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

針對 [**命名空間**]，輸入 "ProductService"。 此選項會定義 proxy 類別的命名空間。

按一下 [ **Go**]。 Visual Studio 讀取 OData 元資料檔案，以探索服務中的實體。

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

按一下 **[確定]** ，將 proxy 類別新增至您的專案。

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>建立服務 Proxy 類別的實例

在 `Main` 方法中，建立 proxy 類別的新實例，如下所示：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

同樣地，請使用您的服務執行所在的實際通訊埠編號。 當您部署服務時，您將會使用 live 服務的 URI。 您不需要更新 proxy。

下列程式碼會新增事件處理常式，以將要求 Uri 列印到主控台視窗。 這不是必要步驟，但要查看每個查詢的 Uri 是很有趣的。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>查詢服務

下列程式碼會從 OData 服務取得產品清單。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

請注意，您不需要撰寫任何程式碼來傳送 HTTP 要求或剖析回應。 當您在**foreach**迴圈中列舉 `Container.Products` 集合時，proxy 類別會自動執行這項工作。

當您執行應用程式時，輸出看起來應該如下所示：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

若要依識別碼取得實體，請使用 `where` 子句。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

在本主題的其餘部分，我將不會顯示整個 `Main` 函式，只是呼叫服務所需的程式碼。

## <a name="apply-query-options"></a>套用查詢選項

OData 定義可用於篩選、排序、分頁資料等的[查詢選項](../supporting-odata-query-options.md)。 在服務 proxy 中，您可以使用各種 LINQ 運算式來套用這些選項。

在本節中，我將示範簡短的範例。 如需詳細資訊，請參閱 MSDN 上的[LINQ 考慮（WCF Data Services）](https://msdn.microsoft.com/library/ee622463.aspx)主題。

### <a name="filtering-filter"></a>篩選（$filter）

若要篩選，請使用 `where` 子句。 下列範例會依產品類別目錄進行篩選。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

此程式碼會對應至下列 OData 查詢。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

請注意，proxy 會將 `where` 子句轉換成 OData `$filter` 運算式。

### <a name="sorting-orderby"></a>排序（$orderby）

若要排序，請使用 `orderby` 子句。 下列範例會依價格排序，從最高到最低。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

以下是對應的 OData 要求。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>用戶端分頁（$skip 和 $top）

對於大型實體集，用戶端可能會想要限制結果的數目。 例如，用戶端可能會一次顯示10個專案。 這稱為*用戶端分頁*。 （也有[伺服器端分頁](../supporting-odata-query-options.md#server-paging)，伺服器會限制結果的數目）。若要執行用戶端分頁，請使用 LINQ **Skip**和**Take**方法。 下列範例會略過前40個結果，並採用下一個10。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

以下是對應的 OData 要求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>選取（$select）並展開（$expand）

若要包含相關實體，請使用 `DataServiceQuery<t>.Expand` 方法。 例如，若要包含每個 `Product`的 `Supplier`：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

以下是對應的 OData 要求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

若要變更回應的圖形，請使用 LINQ **select**子句。 下列範例只會取得每個產品的名稱，沒有其他屬性。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

以下是對應的 OData 要求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 子句可以包含相關的實體。 在此情況下，請勿呼叫**Expand**。在此情況下，proxy 會自動包含擴充。 下列範例會取得每個產品的名稱和供應商。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

以下是對應的 OData 要求。 請注意，它包含 [ **$expand** ] 選項。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

如需 $select 和 $expand 的詳細資訊，請參閱[在 WEB API 2 中使用 $select、$expand 和 $value](../using-select-expand-and-value.md)。

## <a name="add-a-new-entity"></a>加入新的實體

若要將新的實體加入至實體集，請呼叫 `AddToEntitySet`，其中*EntitySet*是實體集的名稱。 例如，`AddToProducts` 會將新的 `Product` 加入至 `Products` 實體集。 當您產生 proxy 時，WCF Data Services 會自動建立這些強型別的**AddTo**方法。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

若要在兩個實體之間新增連結，請使用**AddLink**和**SetLink**方法。 下列程式碼會加入新的供應商和新的產品，然後在它們之間建立連結。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

當導覽屬性為集合時，請使用**AddLink** 。 在此範例中，我們會將產品新增至供應商的 `Products` 集合。

當導覽屬性為單一實體時，請使用**SetLink** 。 在此範例中，我們會設定產品的 `Supplier` 屬性。

## <a name="update--patch"></a>更新/修補程式

若要更新實體，請呼叫**UpdateObject**方法。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

當您呼叫**SaveChanges**時，會執行更新。 根據預設，WCF 會傳送 HTTP MERGE 要求。 **PatchOnUpdate**選項會指示 WCF 改為傳送 HTTP 修補程式。

> [!NOTE]
> 為什麼修補程式與合併？ 原始的 HTTP 1.1 規格（[RCF 2616](http://tools.ietf.org/html/rfc2616)）未定義任何具有「部分更新」語義的 HTTP 方法。 為了支援部分更新，OData 規格定義了 MERGE 方法。 在2010中， [RFC 5789](http://tools.ietf.org/html/rfc5789)定義了部分更新的 PATCH 方法。 您可以在 WCF Data Services 的 Blog 中閱讀這[篇 blog 文章](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)中的部分歷程記錄。 現在，建議您不要透過合併來進行修補。 Web API 樣板所建立的 OData 控制器支援這兩種方法。

如果您想要取代整個實體（PUT 語義），請指定**ReplaceOnUpdate**選項。 這會導致 WCF 傳送 HTTP PUT 要求。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>刪除實體

若要刪除實體，請呼叫**DeleteObject**。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>叫用 OData 動作

在 OData 中，[動作](odata-actions.md)是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。

雖然 OData 元資料檔案會描述這些動作，但 proxy 類別並不會為其建立任何強型別方法。 您仍然可以使用泛型**Execute**方法來叫用 OData 動作。 不過，您必須知道參數的資料類型和傳回值。

例如，`RateProduct` 動作會接受名為「評等」 `Int32` 類型的參數，並傳回 `double`。 下列程式碼說明如何叫用此動作。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

如需詳細資訊，請參閱[呼叫服務作業和動作](https://msdn.microsoft.com/library/hh230677.aspx)。

其中一個選項是擴充**容器**類別，以提供叫用動作的強型別方法：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
