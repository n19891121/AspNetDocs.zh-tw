---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
title: 使用 Web API 2.2 的 OData v4 中的內含專案 |Microsoft Docs
author: rick-anderson
description: 傳統上，只有當實體封裝于實體集內時，才可以存取它。 但是 OData v4 提供兩個額外的選項： Singleton 和 Con .。。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 5fbfefad-a17a-4c46-8646-f1ccd154cd56
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-containment-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 3be81eac9de4686a0d187396e951b121ea65bac4
ms.sourcegitcommit: a4c3c7e04e5f53cf8cd334f036d324976b78d154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84173000"
---
# <a name="containment-in-odata-v4-using-web-api-22"></a>使用 Web API 2.2 的 OData v4 中的內含專案

依 Jinfu Tan

> 傳統上，只有當實體封裝于實體集內時，才可以存取它。 但是 OData v4 提供兩個額外的選項，即 Singleton 和內含專案，兩者都是 WebAPI 2.2 支援的。

本主題說明如何在 WebApi 2.2 中定義 OData 端點的內含專案。 如需內含專案的詳細資訊，請參閱內含專案[隨附于 OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/)。 若要在 Web API 中建立 OData V4 端點，請參閱[使用 ASP.NET Web API 2.2 建立 odata V4 端點](create-an-odata-v4-endpoint.md)。

首先，我們將使用此資料模型，在 OData 服務中建立內含專案領域模型：

![資料模型](odata-containment-in-web-api-22/_static/image1.png)

帳戶包含許多 PaymentInstruments （PI），但我們並未定義 PI 的實體集。 相反地，Pi 只能透過帳戶來存取。

您可以從[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)下載本主題中所使用的解決方案。

## <a name="defining-the-data-model"></a>定義資料模型

1. 定義 CLR 類型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    `Contained`屬性用於內含專案導覽屬性。
2. 根據 CLR 類型產生 EDM 模型。

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    `ODataConventionModelBuilder`如果將 `Contained` 屬性加入至對應的導覽屬性，將會處理建立 EDM 模型。 如果屬性是集合類型， `GetCount(string NameContains)` 也會建立函數。

    產生的中繼資料看起來會像下面這樣：

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    `ContainsTarget`屬性工作表示導覽屬性為內含專案。

## <a name="define-the-containing-entity-set-controller"></a>定義包含的實體集控制器

包含的實體沒有自己的控制器;動作定義于包含實體集控制器中。 在此範例中，有一個 AccountsController，但沒有 PaymentInstrumentsController。

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

如果 OData 路徑是4個或更多區段，只有屬性路由可運作，例如 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 在上述控制器中。 否則，屬性和傳統路由都會運作：例如， `GetPayInPIs(int key)` 符合 `GET ~/Accounts(1)/PayinPIs` 。

*感謝 Leo Hu 這篇文章的原始內容。*
