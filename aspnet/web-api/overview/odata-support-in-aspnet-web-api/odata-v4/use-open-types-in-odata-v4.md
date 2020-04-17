---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: OData v4 中的打開類型,帶有ASP.NET Web API |微軟文件
author: rick-anderson
description: 在 OData v4 中,除了類型定義中聲明的任何屬性外,開放類型是包含動態屬性的結構化類型。 開啟...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d63c96df6614896b3b67eef94a8907e528572567
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543726"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>oData v4 中的開啟類型,具有ASP.NET Web API

由[微軟](https://github.com/microsoft)

> 在 OData v4 中,除了類型定義中聲明的任何屬性外,*開放類型*是包含動態屬性的結構化類型。 打開類型可讓您為數據模型增加靈活性。 本教學示範如何在 Web API OData ASP.NET 中使用開放類型。
> 
> 本教程假定您已經知道如何在ASP.NET Web API 中創建 OData 終結點。 如果沒有,請首先讀取[「創建 OData v4 終結點](create-an-odata-v4-endpoint.md)」。。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教學中使用的軟體版本
> 
> 
> - Web API OData 5.3
> - OData v4

首先,一些 OData 術語:

- 實體類型:具有鍵的結構化類型。
- 複雜類型:沒有鍵的結構化類型。
- 打開類型:具有動態屬性的類型。 實體類型和複雜類型都可以打開。

動態屬性的值可以是基元類型、複雜類型或枚舉類型;因此,動態屬性的值可以是基元類型、複雜類型或枚舉類型。或任何這些類型的集合。 有關開啟類型的詳細資訊,請參閱[OData v4 規範](http://www.odata.org/documentation/odata-version-4-0/)。

## <a name="install-the-web-odata-libraries"></a>安裝 Web OData 函式庫

使用 NuGet 套件管理器安裝最新的 Web API OData 函式庫。 從 [套件管理員主控台] 視窗中：

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>定義 CLR 類型

首先將 EDM 模型定義為 CLR 類型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

創建實體數據模型 (EDM) 時,

- `Category`是枚舉類型。
- `Address`是一種複雜的類型。 (它沒有密鑰,因此它不是實體類型。
- `Customer`是實體類型。 (它有一個鍵。
- `Press`是一種開放的複雜類型。
- `Book`是打開的實體類型。

要建立打開類型,CLR 類型必須具有類型`IDictionary<string, object>`屬性 ,該屬性包含動態屬性。

## <a name="build-the-edm-model"></a>編譯 EDM 模型

如果使用**ODataConventionModelBuilder**創建`Press`EDM, 並且`Book`根據`IDictionary<string, object>`屬性的存在自動添加為打開類型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

您還可以使用**ODataModelBuilder**顯式構建 EDM。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>新增 OData 控制器

接下來,添加 OData 控制器。 在本教學中,我們將使用一個簡化的控制器,該控制器僅支援 GET 和 POST 請求,並使用記憶體中清單來存儲實體。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

請注意,第一`Book`個實例沒有動態屬性。 第二`Book`個實體具有以下動態屬性:

- 已發佈「:原始類型
- 作者":基元型態的集合
- "其他類別":枚舉類型的集合。

此外,該`Press``Book`實體屬性具有以下動態屬性:

- 部落格「:原始類型
- "位址":複雜類型

## <a name="query-the-metadata"></a>查詢中繼資料

要取得 OData 中繼資料文件`~/$metadata`,請傳送 GET 請求。 回應正文應如下所示:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

從中繼資料文件中,您可以看到:

- 對於`Book`和`Press`類型,`OpenType`屬性的值為 true。 `Customer`和`Address`類型沒有此屬性。
- 實體`Book`類型具有三個聲明屬性:ISBN、標題和新聞。 OData 中繼資料不包括`Book.Properties`CLR 類中的屬性。
- 同樣,`Press`複雜類型只有兩個聲明的屬性:名稱和類別。 元數據不包括來自 CLR`Press.DynamicProperties`類的屬性。

## <a name="query-an-entity"></a>查詢實體

要將 ISBN 的書等於「978-0-7356-7942-9」,`~/Books('978-0-7356-7942-9')`請向 發送 GET 請求。 回應正文應類似於以下內容。 (縮進使其更具可讀性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

請注意,動態屬性與聲明的屬性一致。

## <a name="post-an-entity"></a>從實體開始發佈

要添加圖書實體,請向`~/Books`發送 POST 請求。 用戶端可以在請求負載中設置動態屬性。

下面是一個示例請求。 請注意"價格"和"已發佈"屬性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

如果在控制器方法中設定了中斷點,則可以看到 Web API 將這些屬性加入`Properties`字典中 。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>其他資源

[O 資料開啟類型範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
