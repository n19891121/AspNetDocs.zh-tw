---
uid: web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
title: ASP.NET Web API 2.1-ASP.NET 中的 BSON 支援 4.x
author: MikeWasson
description: 示範如何使用 BSON 的 Web API 控制器 （伺服器端） 和.NET 用戶端應用程式中 asp.net 4.x。
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: ce11b017-0ca6-4376-aa9d-a7f3288101de
msc.legacyurl: /web-api/overview/formats-and-model-binding/bson-support-in-web-api-21
msc.type: authoredcontent
ms.openlocfilehash: 911e2abcfd277075b3cba71e624ec6390b99a15e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59382222"
---
# <a name="bson-support-in-aspnet-web-api-21"></a><span data-ttu-id="3a599-103">ASP.NET Web API 2.1 中的 BSON 支援</span><span class="sxs-lookup"><span data-stu-id="3a599-103">BSON Support in ASP.NET Web API 2.1</span></span>

<span data-ttu-id="3a599-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3a599-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3a599-105">本主題說明如何使用.NET 用戶端應用程式和 Web API 控制器中 （伺服器端） 中的 BSON。</span><span class="sxs-lookup"><span data-stu-id="3a599-105">This topic shows how to use BSON in your Web API controller (server side) and in a .NET client app.</span></span> <span data-ttu-id="3a599-106">Web API 2.1 引進了 BSON 支援。</span><span class="sxs-lookup"><span data-stu-id="3a599-106">Web API 2.1 introduces support for BSON.</span></span> 

## <a name="what-is-bson"></a><span data-ttu-id="3a599-107">BSON 是什麼？</span><span class="sxs-lookup"><span data-stu-id="3a599-107">What is BSON?</span></span>

<span data-ttu-id="3a599-108">[BSON](http://bsonspec.org/)是二進位序列化格式。</span><span class="sxs-lookup"><span data-stu-id="3a599-108">[BSON](http://bsonspec.org/) is a binary serialization format.</span></span> <span data-ttu-id="3a599-109">"BSON"代表"二進位 JSON"，但 BSON 和 JSON 序列化非常不同。</span><span class="sxs-lookup"><span data-stu-id="3a599-109">"BSON" stands for "Binary JSON", but BSON and JSON are serialized very differently.</span></span> <span data-ttu-id="3a599-110">BSON 是 「 JSON 類似 」，因為物件以類似 JSON 的名稱 / 值組。</span><span class="sxs-lookup"><span data-stu-id="3a599-110">BSON is "JSON-like", because objects are represented as name-value pairs, similar to JSON.</span></span> <span data-ttu-id="3a599-111">不同於 JSON 中，數值資料類型會儲存為位元組，而不是字串</span><span class="sxs-lookup"><span data-stu-id="3a599-111">Unlike JSON, numeric data types are stored as bytes, not strings</span></span>

<span data-ttu-id="3a599-112">BSON 設計成輕量型、 容易掃描，且速度快，可以編碼/解碼。</span><span class="sxs-lookup"><span data-stu-id="3a599-112">BSON was designed to be lightweight, easy to scan, and fast to encode/decode.</span></span>

- <span data-ttu-id="3a599-113">BSON 相當的大小為 JSON。</span><span class="sxs-lookup"><span data-stu-id="3a599-113">BSON is comparable in size to JSON.</span></span> <span data-ttu-id="3a599-114">根據資料，BSON 承載可能小於或大於 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="3a599-114">Depending on the data, a BSON payload may be smaller or larger than a JSON payload.</span></span> <span data-ttu-id="3a599-115">序列化二進位資料，例如影像檔，因為二進位資料不是 base64 編碼，會小於 JSON、 BSON。</span><span class="sxs-lookup"><span data-stu-id="3a599-115">For serializing binary data, such as an image file, BSON is smaller than JSON, because the binary data is not base64-encoded.</span></span>
- <span data-ttu-id="3a599-116">BSON 文件很容易就能掃描，因為項目會加上 [長度] 欄位中，因此剖析器可以略過項目而不需要加以解碼。</span><span class="sxs-lookup"><span data-stu-id="3a599-116">BSON documents are easy to scan because elements are prefixed with a length field, so a parser can skip elements without decoding them.</span></span>
- <span data-ttu-id="3a599-117">編碼和解碼會有效率，因為數值資料類型會儲存成數字，不是字串。</span><span class="sxs-lookup"><span data-stu-id="3a599-117">Encoding and decoding are efficient, because numeric data types are stored as numbers, not strings.</span></span>

<span data-ttu-id="3a599-118">原生用戶端，例如.NET 用戶端應用程式，可以受益於使用 BSON 取代文字為基礎的格式，例如 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="3a599-118">Native clients, such as .NET client apps, can benefit from using BSON in place of text-based formats such as JSON or XML.</span></span> <span data-ttu-id="3a599-119">瀏覽器用戶端，您可能要堅持使用 JSON，因為 JavaScript 可以直接將轉換的 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="3a599-119">For browser clients, you will probably want to stick with JSON, because JavaScript can directly convert the JSON payload.</span></span>

<span data-ttu-id="3a599-120">幸運的是，Web API 會使用[內容交涉](content-negotiation.md)，因此您的 API 可以支援這兩種格式，並讓選擇的用戶端。</span><span class="sxs-lookup"><span data-stu-id="3a599-120">Fortunately, Web API uses [content negotiation](content-negotiation.md), so your API can support both formats and let the client choose.</span></span>

## <a name="enabling-bson-on-the-server"></a><span data-ttu-id="3a599-121">啟用在伺服器上的 BSON</span><span class="sxs-lookup"><span data-stu-id="3a599-121">Enabling BSON on the Server</span></span>

<span data-ttu-id="3a599-122">在 Web API 組態中，新增**BsonMediaTypeFormatter**格式器集合。</span><span class="sxs-lookup"><span data-stu-id="3a599-122">In your Web API configuration, add the **BsonMediaTypeFormatter** to the formatters collection.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample1.cs)]

<span data-ttu-id="3a599-123">現在如果用戶端要求為"application/bson"，則 Web API 會使用 BSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="3a599-123">Now if the client requests "application/bson", Web API will use the BSON formatter.</span></span>

<span data-ttu-id="3a599-124">若要關聯 BSON 與其他媒體類型，將它們加入 SupportedMediaTypes 集合。</span><span class="sxs-lookup"><span data-stu-id="3a599-124">To associate BSON with other media types, add them to the SupportedMediaTypes collection.</span></span> <span data-ttu-id="3a599-125">下列程式碼會將 「 application/vnd.contoso"新增至支援的媒體類型：</span><span class="sxs-lookup"><span data-stu-id="3a599-125">The following code adds "application/vnd.contoso" to the supported media types:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample2.cs)]

## <a name="example-http-session"></a><span data-ttu-id="3a599-126">範例 HTTP 工作階段</span><span class="sxs-lookup"><span data-stu-id="3a599-126">Example HTTP Session</span></span>

<span data-ttu-id="3a599-127">此範例中，我們將使用下列模型類別加上簡單的 Web API 控制器：</span><span class="sxs-lookup"><span data-stu-id="3a599-127">For this example, we'll use the following model class plus a simple Web API controller:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample3.cs)]

<span data-ttu-id="3a599-128">用戶端可能會傳送下列 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="3a599-128">A client might send the following HTTP request:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample4.cmd)]

<span data-ttu-id="3a599-129">以下是回應：</span><span class="sxs-lookup"><span data-stu-id="3a599-129">Here is the response:</span></span>

[!code-console[Main](bson-support-in-web-api-21/samples/sample5.cmd)]

<span data-ttu-id="3a599-130">此處我已被取代的二進位資料， &quot;。&quot;字元。</span><span class="sxs-lookup"><span data-stu-id="3a599-130">Here I've replaced the binary data with &quot;.&quot; characters.</span></span> <span data-ttu-id="3a599-131">下列螢幕擷取畫面所示 Fiddler 的未經處理的十六進位值。</span><span class="sxs-lookup"><span data-stu-id="3a599-131">The following screen shot from Fiddler shows the raw hex values.</span></span>

[![](bson-support-in-web-api-21/_static/image2.png)](bson-support-in-web-api-21/_static/image1.png)

## <a name="using-bson-with-httpclient"></a><span data-ttu-id="3a599-132">BSON 使用 HttpClient</span><span class="sxs-lookup"><span data-stu-id="3a599-132">Using BSON with HttpClient</span></span>

<span data-ttu-id="3a599-133">.NET 用戶端應用程式可以使用 BSON 格式器，與**HttpClient**。</span><span class="sxs-lookup"><span data-stu-id="3a599-133">.NET clients apps can use the BSON formatter with **HttpClient**.</span></span> <span data-ttu-id="3a599-134">如需詳細資訊**HttpClient**，請參閱[呼叫 Web API 從.NET 用戶端](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="3a599-134">For more information about **HttpClient**, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="3a599-135">下列程式碼會傳送 GET 要求，以便接受 BSON，並接著會在回應中的 BSON 承載還原序列化。</span><span class="sxs-lookup"><span data-stu-id="3a599-135">The following code sends a GET request that accepts BSON, and then deserializes the BSON payload in the response.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample6.cs)]

<span data-ttu-id="3a599-136">若要從伺服器要求 BSON，設定為"application/bson"Accept 標頭：</span><span class="sxs-lookup"><span data-stu-id="3a599-136">To request BSON from the server, set the Accept header to "application/bson":</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample7.cs)]

<span data-ttu-id="3a599-137">若要還原序列化回應主體，請使用**BsonMediaTypeFormatter**。</span><span class="sxs-lookup"><span data-stu-id="3a599-137">To deserialize the response body, use the **BsonMediaTypeFormatter**.</span></span> <span data-ttu-id="3a599-138">此格式器不是在預設格式器集合中，因此您必須指定它時讀取回應主體：</span><span class="sxs-lookup"><span data-stu-id="3a599-138">This formatter is not in the default formatters collection, so you have to specify it when you read the response body:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample8.cs)]

<span data-ttu-id="3a599-139">下一個範例示範如何傳送 POST 要求，其中包含 BSON。</span><span class="sxs-lookup"><span data-stu-id="3a599-139">The next example shows how to send a POST request that contains BSON.</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample9.cs)]

<span data-ttu-id="3a599-140">此程式碼大多是與前一個範例相同。</span><span class="sxs-lookup"><span data-stu-id="3a599-140">Much of this code is the same as the previous example.</span></span> <span data-ttu-id="3a599-141">但在**PostAsync**方法，指定**BsonMediaTypeFormatter**格式器為：</span><span class="sxs-lookup"><span data-stu-id="3a599-141">But in the **PostAsync** method, specify **BsonMediaTypeFormatter** as the formatter:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample10.cs)]

## <a name="serializing-top-level-primitive-types"></a><span data-ttu-id="3a599-142">序列化的最上層基本型別</span><span class="sxs-lookup"><span data-stu-id="3a599-142">Serializing Top-Level Primitive Types</span></span>

<span data-ttu-id="3a599-143">每個 BSON 文件是索引鍵/值組清單。BSON 規格並未定義序列化單一的原始值，例如整數或字串的語法。</span><span class="sxs-lookup"><span data-stu-id="3a599-143">Every BSON document is a list of key/value pairs.The BSON specification does not define a syntax for serializing a single raw value, such as an integer or string.</span></span>

<span data-ttu-id="3a599-144">若要解決此限制，請**BsonMediaTypeFormatter**視為特殊案例中的基本型別。</span><span class="sxs-lookup"><span data-stu-id="3a599-144">To work around this limitation, the **BsonMediaTypeFormatter** treats primitive types as a special case.</span></span> <span data-ttu-id="3a599-145">序列化之前, 它會將值轉換的索引鍵/值組與 「 值 」 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3a599-145">Before serializing, it converts the value into a key/value pair with the key "Value".</span></span> <span data-ttu-id="3a599-146">例如，假設您的 API 控制器會傳回一個整數：</span><span class="sxs-lookup"><span data-stu-id="3a599-146">For example, suppose your API controller returns an integer:</span></span>

[!code-csharp[Main](bson-support-in-web-api-21/samples/sample11.cs)]

<span data-ttu-id="3a599-147">序列化之前, 的 BSON 格式器會將這下列索引鍵/值組：</span><span class="sxs-lookup"><span data-stu-id="3a599-147">Before serializing, the BSON formatter converts this to the following key/value pair:</span></span>

[!code-json[Main](bson-support-in-web-api-21/samples/sample12.json)]

<span data-ttu-id="3a599-148">當您還原序列化時，格式器會將資料轉換回原始的值。</span><span class="sxs-lookup"><span data-stu-id="3a599-148">When you deserialize, the formatter converts the data back to the original value.</span></span> <span data-ttu-id="3a599-149">不過，使用不同的 BSON 剖析器用戶端必須處理這種情況，如果您的 web API 會傳回原始值。</span><span class="sxs-lookup"><span data-stu-id="3a599-149">However, clients using a different BSON parser will need to handle this case, if your web API returns raw values.</span></span> <span data-ttu-id="3a599-150">一般情況下，您應該考慮傳回結構化的資料，而不是原始的值。</span><span class="sxs-lookup"><span data-stu-id="3a599-150">In general, you should consider returning structured data, rather than raw values.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a599-151">其他資源</span><span class="sxs-lookup"><span data-stu-id="3a599-151">Additional Resources</span></span>

[<span data-ttu-id="3a599-152">Web API BSON 範例</span><span class="sxs-lookup"><span data-stu-id="3a599-152">Web API BSON Sample</span></span>](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/BSONSample/)

[<span data-ttu-id="3a599-153">媒體格式器</span><span class="sxs-lookup"><span data-stu-id="3a599-153">Media Formatters</span></span>](media-formatters.md)
