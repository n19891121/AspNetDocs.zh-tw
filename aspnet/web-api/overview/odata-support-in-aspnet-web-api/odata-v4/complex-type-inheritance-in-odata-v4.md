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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="1710c-104">使用ASP.NET Web API 的 OData v4 中的複雜類型繼承</span><span class="sxs-lookup"><span data-stu-id="1710c-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="1710c-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1710c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1710c-106">根據 OData v4[規範](http://www.odata.org/documentation/odata-version-4-0/),複雜類型可以從另一種複雜類型繼承。</span><span class="sxs-lookup"><span data-stu-id="1710c-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="1710c-107">(*複雜*類型是無鍵的結構化類型。Web API OData 5.3 支援複雜的類型繼承。</span><span class="sxs-lookup"><span data-stu-id="1710c-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="1710c-108">本主題示範如何構建具有複雜繼承類型的實體數據模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="1710c-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="1710c-109">有關完整的原始碼,請參考[OData 複雜類型繼承範例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="1710c-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1710c-110">本教學中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="1710c-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1710c-111">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="1710c-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="1710c-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="1710c-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="1710c-113">模型層次結構</span><span class="sxs-lookup"><span data-stu-id="1710c-113">Model Hierarchy</span></span>

<span data-ttu-id="1710c-114">為了說明複雜的類型繼承,我們將使用以下類層次結構。</span><span class="sxs-lookup"><span data-stu-id="1710c-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="1710c-115">`Shape`是一種抽象的複雜類型。</span><span class="sxs-lookup"><span data-stu-id="1710c-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="1710c-116">`Rectangle``Triangle`與`Circle`從 派`Shape`生的複雜類型,`RoundRectangle`並且 派`Rectangle`生自 。</span><span class="sxs-lookup"><span data-stu-id="1710c-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="1710c-117">`Window`是實體類型,包含實體`Shape`。</span><span class="sxs-lookup"><span data-stu-id="1710c-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="1710c-118">下面是定義這些類型的CLR類。</span><span class="sxs-lookup"><span data-stu-id="1710c-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="1710c-119">編譯 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="1710c-119">Build the EDM Model</span></span>

<span data-ttu-id="1710c-120">要創建 EDM,可以使用**ODataConventionModelBuilder**,它推斷出 CLR 類型的繼承關係。</span><span class="sxs-lookup"><span data-stu-id="1710c-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="1710c-121">您還可以使用**ODataModelBuilder**顯式構建 EDM。</span><span class="sxs-lookup"><span data-stu-id="1710c-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="1710c-122">這需要更多的代碼,但使您能夠對 EDM 進行更多的控制。</span><span class="sxs-lookup"><span data-stu-id="1710c-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="1710c-123">這兩個範例創建相同的 EDM 架構。</span><span class="sxs-lookup"><span data-stu-id="1710c-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="1710c-124">中繼資料文件</span><span class="sxs-lookup"><span data-stu-id="1710c-124">Metadata Document</span></span>

<span data-ttu-id="1710c-125">下面是 OData 中數據文件,顯示複雜的類型繼承。</span><span class="sxs-lookup"><span data-stu-id="1710c-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="1710c-126">從中繼資料文件中,您可以看到:</span><span class="sxs-lookup"><span data-stu-id="1710c-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="1710c-127">複雜`Shape`類型是抽象的。</span><span class="sxs-lookup"><span data-stu-id="1710c-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="1710c-128">`Triangle``Rectangle`與`Circle`複合類型具有基型`Shape`態 。</span><span class="sxs-lookup"><span data-stu-id="1710c-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="1710c-129">類型`RoundRectangle`有基`Rectangle`型態 。</span><span class="sxs-lookup"><span data-stu-id="1710c-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="1710c-130">鑄造複雜類型</span><span class="sxs-lookup"><span data-stu-id="1710c-130">Casting Complex Types</span></span>

<span data-ttu-id="1710c-131">現在支援對複雜類型的強制轉換。</span><span class="sxs-lookup"><span data-stu-id="1710c-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="1710c-132">例如,以下查詢將 轉換`Shape`為`Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="1710c-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="1710c-133">下面是回應負載:</span><span class="sxs-lookup"><span data-stu-id="1710c-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
