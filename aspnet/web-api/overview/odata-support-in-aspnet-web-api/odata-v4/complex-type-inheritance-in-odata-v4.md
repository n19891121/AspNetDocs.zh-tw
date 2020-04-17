---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 使用ASP.NET Web API 的 OData v4 中的複雜類型繼承 |微軟文件
author: rick-anderson
description: 根據 OData v4 規範,複雜類型可以從另一種複雜類型繼承。 (複雜類型是無鍵的結構化類型。Web API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: f433cf625c7d6ff4922d8c4a9954682fc0f1cc33
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543596"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>使用ASP.NET Web API 的 OData v4 中的複雜類型繼承

由[微軟](https://github.com/microsoft)

> 根據 OData v4[規範](http://www.odata.org/documentation/odata-version-4-0/),複雜類型可以從另一種複雜類型繼承。 (*複雜*類型是無鍵的結構化類型。Web API OData 5.3 支援複雜的類型繼承。
> 
> 本主題示範如何構建具有複雜繼承類型的實體數據模型 (EDM)。 有關完整的原始碼,請參考[OData 複雜類型繼承範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教學中使用的軟體版本
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>模型層次結構

為了說明複雜的類型繼承,我們將使用以下類層次結構。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`是一種抽象的複雜類型。 `Rectangle``Triangle`與`Circle`從 派`Shape`生的複雜類型,`RoundRectangle`並且 派`Rectangle`生自 。 `Window`是實體類型,包含實體`Shape`。

下面是定義這些類型的CLR類。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>編譯 EDM 模型

要創建 EDM,可以使用**ODataConventionModelBuilder**,它推斷出 CLR 類型的繼承關係。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

您還可以使用**ODataModelBuilder**顯式構建 EDM。 這需要更多的代碼,但使您能夠對 EDM 進行更多的控制。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

這兩個範例創建相同的 EDM 架構。

## <a name="metadata-document"></a>中繼資料文件

下面是 OData 中數據文件,顯示複雜的類型繼承。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

從中繼資料文件中,您可以看到:

- 複雜`Shape`類型是抽象的。
- `Triangle``Rectangle`與`Circle`複合類型具有基型`Shape`態 。
- 類型`RoundRectangle`有基`Rectangle`型態 。

## <a name="casting-complex-types"></a>鑄造複雜類型

現在支援對複雜類型的強制轉換。 例如,以下查詢將 轉換`Shape`為`Rectangle`。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

下面是回應負載:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
