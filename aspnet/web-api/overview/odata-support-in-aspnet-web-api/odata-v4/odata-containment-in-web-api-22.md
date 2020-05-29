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
# <a name="containment-in-odata-v4-using-web-api-22"></a><span data-ttu-id="014c7-104">使用 Web API 2.2 的 OData v4 中的內含專案</span><span class="sxs-lookup"><span data-stu-id="014c7-104">Containment in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="014c7-105">依 Jinfu Tan</span><span class="sxs-lookup"><span data-stu-id="014c7-105">by Jinfu Tan</span></span>

> <span data-ttu-id="014c7-106">傳統上，只有當實體封裝于實體集內時，才可以存取它。</span><span class="sxs-lookup"><span data-stu-id="014c7-106">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="014c7-107">但是 OData v4 提供兩個額外的選項，即 Singleton 和內含專案，兩者都是 WebAPI 2.2 支援的。</span><span class="sxs-lookup"><span data-stu-id="014c7-107">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="014c7-108">本主題說明如何在 WebApi 2.2 中定義 OData 端點的內含專案。</span><span class="sxs-lookup"><span data-stu-id="014c7-108">This topic shows how to define a containment in an OData endpoint in WebApi 2.2.</span></span> <span data-ttu-id="014c7-109">如需內含專案的詳細資訊，請參閱內含專案[隨附于 OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/)。</span><span class="sxs-lookup"><span data-stu-id="014c7-109">For more information about containment, see [Containment is coming with OData v4](https://devblogs.microsoft.com/odata/tutorial-sample-containment-is-coming-with-odata-v4/).</span></span> <span data-ttu-id="014c7-110">若要在 Web API 中建立 OData V4 端點，請參閱[使用 ASP.NET Web API 2.2 建立 odata V4 端點](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="014c7-110">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="014c7-111">首先，我們將使用此資料模型，在 OData 服務中建立內含專案領域模型：</span><span class="sxs-lookup"><span data-stu-id="014c7-111">First, we'll create a containment domain model in the OData service, using this data model:</span></span>

![資料模型](odata-containment-in-web-api-22/_static/image1.png)

<span data-ttu-id="014c7-113">帳戶包含許多 PaymentInstruments （PI），但我們並未定義 PI 的實體集。</span><span class="sxs-lookup"><span data-stu-id="014c7-113">An account contains many PaymentInstruments (PI), but we don't define an entity set for a PI.</span></span> <span data-ttu-id="014c7-114">相反地，Pi 只能透過帳戶來存取。</span><span class="sxs-lookup"><span data-stu-id="014c7-114">Instead, the PIs can only be accessed through an Account.</span></span>

<span data-ttu-id="014c7-115">您可以從[CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)下載本主題中所使用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="014c7-115">You can download the solution used in this topic from [CodePlex](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/).</span></span>

## <a name="defining-the-data-model"></a><span data-ttu-id="014c7-116">定義資料模型</span><span class="sxs-lookup"><span data-stu-id="014c7-116">Defining the data model</span></span>

1. <span data-ttu-id="014c7-117">定義 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="014c7-117">Define the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample1.cs)]

    <span data-ttu-id="014c7-118">`Contained`屬性用於內含專案導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="014c7-118">The `Contained` attribute is used for containment navigation properties.</span></span>
2. <span data-ttu-id="014c7-119">根據 CLR 類型產生 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="014c7-119">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](odata-containment-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="014c7-120">`ODataConventionModelBuilder`如果將 `Contained` 屬性加入至對應的導覽屬性，將會處理建立 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="014c7-120">The `ODataConventionModelBuilder` will handle building the EDM model if the `Contained` attribute is added to the corresponding navigation property.</span></span> <span data-ttu-id="014c7-121">如果屬性是集合類型， `GetCount(string NameContains)` 也會建立函數。</span><span class="sxs-lookup"><span data-stu-id="014c7-121">If the property is a collection type, a `GetCount(string NameContains)` function will also be created.</span></span>

    <span data-ttu-id="014c7-122">產生的中繼資料看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="014c7-122">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](odata-containment-in-web-api-22/samples/sample3.xml?highlight=10)]

    <span data-ttu-id="014c7-123">`ContainsTarget`屬性工作表示導覽屬性為內含專案。</span><span class="sxs-lookup"><span data-stu-id="014c7-123">The `ContainsTarget` attribute indicates that the navigation property is a containment.</span></span>

## <a name="define-the-containing-entity-set-controller"></a><span data-ttu-id="014c7-124">定義包含的實體集控制器</span><span class="sxs-lookup"><span data-stu-id="014c7-124">Define the containing entity set controller</span></span>

<span data-ttu-id="014c7-125">包含的實體沒有自己的控制器;動作定義于包含實體集控制器中。</span><span class="sxs-lookup"><span data-stu-id="014c7-125">Contained entities don't have their own controller; the action is defined in the containing entity set controller.</span></span> <span data-ttu-id="014c7-126">在此範例中，有一個 AccountsController，但沒有 PaymentInstrumentsController。</span><span class="sxs-lookup"><span data-stu-id="014c7-126">In this sample, there is an AccountsController, but no PaymentInstrumentsController.</span></span>

[!code-csharp[Main](odata-containment-in-web-api-22/samples/sample4.cs)]

<span data-ttu-id="014c7-127">如果 OData 路徑是4個或更多區段，只有屬性路由可運作，例如 `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` 在上述控制器中。</span><span class="sxs-lookup"><span data-stu-id="014c7-127">If the OData path is 4 or more segments, only attribute routing works, such as `[ODataRoute("Accounts({accountId})/PayinPIs({paymentInstrumentId})")]` in the above controller.</span></span> <span data-ttu-id="014c7-128">否則，屬性和傳統路由都會運作：例如， `GetPayInPIs(int key)` 符合 `GET ~/Accounts(1)/PayinPIs` 。</span><span class="sxs-lookup"><span data-stu-id="014c7-128">Otherwise, both attribute and conventional routing works: for instance, `GetPayInPIs(int key)` matches `GET ~/Accounts(1)/PayinPIs`.</span></span>

<span data-ttu-id="014c7-129">*感謝 Leo Hu 這篇文章的原始內容。*</span><span class="sxs-lookup"><span data-stu-id="014c7-129">*Thanks to Leo Hu for the original content of this article.*</span></span>
