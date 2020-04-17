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
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="c3a20-104">oData v4 中的開啟類型,具有ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="c3a20-104">Open Types in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="c3a20-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c3a20-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c3a20-106">在 OData v4 中,除了類型定義中聲明的任何屬性外,*開放類型*是包含動態屬性的結構化類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-106">In OData v4, an *open type* is a structured type that contains dynamic properties, in addition to any properties that are declared in the type definition.</span></span> <span data-ttu-id="c3a20-107">打開類型可讓您為數據模型增加靈活性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-107">Open types let you add flexibility to your data models.</span></span> <span data-ttu-id="c3a20-108">本教學示範如何在 Web API OData ASP.NET 中使用開放類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-108">This tutorial shows how to use open types in ASP.NET Web API OData.</span></span>
> 
> <span data-ttu-id="c3a20-109">本教程假定您已經知道如何在ASP.NET Web API 中創建 OData 終結點。</span><span class="sxs-lookup"><span data-stu-id="c3a20-109">This tutorial assumes that you already know how to create an OData endpoint in ASP.NET Web API.</span></span> <span data-ttu-id="c3a20-110">如果沒有,請首先讀取[「創建 OData v4 終結點](create-an-odata-v4-endpoint.md)」。。</span><span class="sxs-lookup"><span data-stu-id="c3a20-110">If not, start by reading [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md) first.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c3a20-111">本教學中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="c3a20-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c3a20-112">Web API OData 5.3</span><span class="sxs-lookup"><span data-stu-id="c3a20-112">Web API OData 5.3</span></span>
> - <span data-ttu-id="c3a20-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="c3a20-113">OData v4</span></span>

<span data-ttu-id="c3a20-114">首先,一些 OData 術語:</span><span class="sxs-lookup"><span data-stu-id="c3a20-114">First, some OData terminology:</span></span>

- <span data-ttu-id="c3a20-115">實體類型:具有鍵的結構化類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-115">Entity type: A structured type with a key.</span></span>
- <span data-ttu-id="c3a20-116">複雜類型:沒有鍵的結構化類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-116">Complex type: A structured type without a key.</span></span>
- <span data-ttu-id="c3a20-117">打開類型:具有動態屬性的類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-117">Open type: A type with dynamic properties.</span></span> <span data-ttu-id="c3a20-118">實體類型和複雜類型都可以打開。</span><span class="sxs-lookup"><span data-stu-id="c3a20-118">Both entity types and complex types can be open.</span></span>

<span data-ttu-id="c3a20-119">動態屬性的值可以是基元類型、複雜類型或枚舉類型;因此,動態屬性的值可以是基元類型、複雜類型或枚舉類型。或任何這些類型的集合。</span><span class="sxs-lookup"><span data-stu-id="c3a20-119">The value of a dynamic property can be a primitive type, complex type, or enumeration type; or a collection of any of those types.</span></span> <span data-ttu-id="c3a20-120">有關開啟類型的詳細資訊,請參閱[OData v4 規範](http://www.odata.org/documentation/odata-version-4-0/)。</span><span class="sxs-lookup"><span data-stu-id="c3a20-120">For more information about open types, see the [OData v4 specification](http://www.odata.org/documentation/odata-version-4-0/).</span></span>

## <a name="install-the-web-odata-libraries"></a><span data-ttu-id="c3a20-121">安裝 Web OData 函式庫</span><span class="sxs-lookup"><span data-stu-id="c3a20-121">Install the Web OData Libraries</span></span>

<span data-ttu-id="c3a20-122">使用 NuGet 套件管理器安裝最新的 Web API OData 函式庫。</span><span class="sxs-lookup"><span data-stu-id="c3a20-122">Use NuGet Package Manager to install the latest Web API OData libraries.</span></span> <span data-ttu-id="c3a20-123">從 [套件管理員主控台] 視窗中：</span><span class="sxs-lookup"><span data-stu-id="c3a20-123">From the Package Manager Console window:</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a><span data-ttu-id="c3a20-124">定義 CLR 類型</span><span class="sxs-lookup"><span data-stu-id="c3a20-124">Define the CLR Types</span></span>

<span data-ttu-id="c3a20-125">首先將 EDM 模型定義為 CLR 類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-125">Start by defining the EDM models as CLR types.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="c3a20-126">創建實體數據模型 (EDM) 時,</span><span class="sxs-lookup"><span data-stu-id="c3a20-126">When the Entity Data Model (EDM) is created,</span></span>

- <span data-ttu-id="c3a20-127">`Category`是枚舉類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-127">`Category` is an enumeration type.</span></span>
- <span data-ttu-id="c3a20-128">`Address`是一種複雜的類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-128">`Address` is a complex type.</span></span> <span data-ttu-id="c3a20-129">(它沒有密鑰,因此它不是實體類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-129">(It does not have a key, so it is not an entity type.)</span></span>
- <span data-ttu-id="c3a20-130">`Customer`是實體類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-130">`Customer` is an entity type.</span></span> <span data-ttu-id="c3a20-131">(它有一個鍵。</span><span class="sxs-lookup"><span data-stu-id="c3a20-131">(It has a key.)</span></span>
- <span data-ttu-id="c3a20-132">`Press`是一種開放的複雜類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-132">`Press` is an open complex type.</span></span>
- <span data-ttu-id="c3a20-133">`Book`是打開的實體類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-133">`Book` is an open entity type.</span></span>

<span data-ttu-id="c3a20-134">要建立打開類型,CLR 類型必須具有類型`IDictionary<string, object>`屬性 ,該屬性包含動態屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-134">To create an open type, the CLR type must have a property of type `IDictionary<string, object>`, which holds the dynamic properties.</span></span>

## <a name="build-the-edm-model"></a><span data-ttu-id="c3a20-135">編譯 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="c3a20-135">Build the EDM Model</span></span>

<span data-ttu-id="c3a20-136">如果使用**ODataConventionModelBuilder**創建`Press`EDM, 並且`Book`根據`IDictionary<string, object>`屬性的存在自動添加為打開類型。</span><span class="sxs-lookup"><span data-stu-id="c3a20-136">If you use **ODataConventionModelBuilder** to create the EDM, `Press` and `Book` are automatically added as open types, based on the presence of a `IDictionary<string, object>` property.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="c3a20-137">您還可以使用**ODataModelBuilder**顯式構建 EDM。</span><span class="sxs-lookup"><span data-stu-id="c3a20-137">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a><span data-ttu-id="c3a20-138">新增 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="c3a20-138">Add an OData Controller</span></span>

<span data-ttu-id="c3a20-139">接下來,添加 OData 控制器。</span><span class="sxs-lookup"><span data-stu-id="c3a20-139">Next, add an OData controller.</span></span> <span data-ttu-id="c3a20-140">在本教學中,我們將使用一個簡化的控制器,該控制器僅支援 GET 和 POST 請求,並使用記憶體中清單來存儲實體。</span><span class="sxs-lookup"><span data-stu-id="c3a20-140">For this tutorial, we'll use a simplified controller that just supports GET and POST requests, and uses an in-memory list to store entities.</span></span>

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="c3a20-141">請注意,第一`Book`個實例沒有動態屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-141">Notice that the first `Book` instance has no dynamic properties.</span></span> <span data-ttu-id="c3a20-142">第二`Book`個實體具有以下動態屬性:</span><span class="sxs-lookup"><span data-stu-id="c3a20-142">The second `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="c3a20-143">已發佈「:原始類型</span><span class="sxs-lookup"><span data-stu-id="c3a20-143">"Published": Primitive type</span></span>
- <span data-ttu-id="c3a20-144">作者":基元型態的集合</span><span class="sxs-lookup"><span data-stu-id="c3a20-144">"Authors": Collection of primitive types</span></span>
- <span data-ttu-id="c3a20-145">"其他類別":枚舉類型的集合。</span><span class="sxs-lookup"><span data-stu-id="c3a20-145">"OtherCategories": Collection of enumeration types.</span></span>

<span data-ttu-id="c3a20-146">此外,該`Press``Book`實體屬性具有以下動態屬性:</span><span class="sxs-lookup"><span data-stu-id="c3a20-146">Also, the `Press` property of that `Book` instance has the following dynamic properties:</span></span>

- <span data-ttu-id="c3a20-147">部落格「:原始類型</span><span class="sxs-lookup"><span data-stu-id="c3a20-147">"Blog": Primitive type</span></span>
- <span data-ttu-id="c3a20-148">"位址":複雜類型</span><span class="sxs-lookup"><span data-stu-id="c3a20-148">"Address": Complex type</span></span>

## <a name="query-the-metadata"></a><span data-ttu-id="c3a20-149">查詢中繼資料</span><span class="sxs-lookup"><span data-stu-id="c3a20-149">Query the Metadata</span></span>

<span data-ttu-id="c3a20-150">要取得 OData 中繼資料文件`~/$metadata`,請傳送 GET 請求。</span><span class="sxs-lookup"><span data-stu-id="c3a20-150">To get the OData metadata document, send a GET request to `~/$metadata`.</span></span> <span data-ttu-id="c3a20-151">回應正文應如下所示:</span><span class="sxs-lookup"><span data-stu-id="c3a20-151">The response body should look similar to this:</span></span>

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

<span data-ttu-id="c3a20-152">從中繼資料文件中,您可以看到:</span><span class="sxs-lookup"><span data-stu-id="c3a20-152">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="c3a20-153">對於`Book`和`Press`類型,`OpenType`屬性的值為 true。</span><span class="sxs-lookup"><span data-stu-id="c3a20-153">For the `Book` and `Press` types, the value of the `OpenType` attribute is true.</span></span> <span data-ttu-id="c3a20-154">`Customer`和`Address`類型沒有此屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-154">The `Customer` and `Address` types don't have this attribute.</span></span>
- <span data-ttu-id="c3a20-155">實體`Book`類型具有三個聲明屬性:ISBN、標題和新聞。</span><span class="sxs-lookup"><span data-stu-id="c3a20-155">The `Book` entity type has three declared properties: ISBN, Title, and Press.</span></span> <span data-ttu-id="c3a20-156">OData 中繼資料不包括`Book.Properties`CLR 類中的屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-156">The OData metadata does not include the `Book.Properties` property from the CLR class.</span></span>
- <span data-ttu-id="c3a20-157">同樣,`Press`複雜類型只有兩個聲明的屬性:名稱和類別。</span><span class="sxs-lookup"><span data-stu-id="c3a20-157">Similarly, the `Press` complex type has only two declared properties: Name and Category.</span></span> <span data-ttu-id="c3a20-158">元數據不包括來自 CLR`Press.DynamicProperties`類的屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-158">The metadata does not include the `Press.DynamicProperties` property from the CLR class.</span></span>

## <a name="query-an-entity"></a><span data-ttu-id="c3a20-159">查詢實體</span><span class="sxs-lookup"><span data-stu-id="c3a20-159">Query an Entity</span></span>

<span data-ttu-id="c3a20-160">要將 ISBN 的書等於「978-0-7356-7942-9」,`~/Books('978-0-7356-7942-9')`請向 發送 GET 請求。</span><span class="sxs-lookup"><span data-stu-id="c3a20-160">To get the book with ISBN equal to "978-0-7356-7942-9", send a GET request to `~/Books('978-0-7356-7942-9')`.</span></span> <span data-ttu-id="c3a20-161">回應正文應類似於以下內容。</span><span class="sxs-lookup"><span data-stu-id="c3a20-161">The response body should look similar to the following.</span></span> <span data-ttu-id="c3a20-162">(縮進使其更具可讀性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-162">(Indented to make it more readable.)</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

<span data-ttu-id="c3a20-163">請注意,動態屬性與聲明的屬性一致。</span><span class="sxs-lookup"><span data-stu-id="c3a20-163">Notice that the dynamic properties are included inline with the declared properties.</span></span>

## <a name="post-an-entity"></a><span data-ttu-id="c3a20-164">從實體開始發佈</span><span class="sxs-lookup"><span data-stu-id="c3a20-164">POST an Entity</span></span>

<span data-ttu-id="c3a20-165">要添加圖書實體,請向`~/Books`發送 POST 請求。</span><span class="sxs-lookup"><span data-stu-id="c3a20-165">To add a Book entity, send a POST request to `~/Books`.</span></span> <span data-ttu-id="c3a20-166">用戶端可以在請求負載中設置動態屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-166">The client can set dynamic properties in the request payload.</span></span>

<span data-ttu-id="c3a20-167">下面是一個示例請求。</span><span class="sxs-lookup"><span data-stu-id="c3a20-167">Here is an example request.</span></span> <span data-ttu-id="c3a20-168">請注意"價格"和"已發佈"屬性。</span><span class="sxs-lookup"><span data-stu-id="c3a20-168">Note the "Price" and "Published" properties.</span></span>

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

<span data-ttu-id="c3a20-169">如果在控制器方法中設定了中斷點,則可以看到 Web API 將這些屬性加入`Properties`字典中 。</span><span class="sxs-lookup"><span data-stu-id="c3a20-169">If you set a breakpoint in the controller method, you can see that Web API added these properties to the `Properties` dictionary.</span></span>

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="c3a20-170">其他資源</span><span class="sxs-lookup"><span data-stu-id="c3a20-170">Additional Resources</span></span>

[<span data-ttu-id="c3a20-171">O 資料開啟類型範例</span><span class="sxs-lookup"><span data-stu-id="c3a20-171">OData Open Type Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
