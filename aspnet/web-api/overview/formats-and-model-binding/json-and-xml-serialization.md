---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API 中的 JSON 和 XML 序列化 - ASP.NET 4.x
author: MikeWasson
description: 描述ASP.NET 4.x ASP.NET Web API 中的 JSON 和 XML for物質。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676220"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="96e1a-103">ASP.NET Web API 中的 JSON 和 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="96e1a-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="96e1a-104">由[邁克·瓦森](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="96e1a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="96e1a-105">本文介紹了ASP.NET Web API 中的 JSON 和 XML 等事。</span><span class="sxs-lookup"><span data-stu-id="96e1a-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="96e1a-106">在 Web API ASP.NET,*媒體類型的前物質*是一個物件,可以:</span><span class="sxs-lookup"><span data-stu-id="96e1a-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="96e1a-107">從 HTTP 訊息正課程讀取 CLR 物件</span><span class="sxs-lookup"><span data-stu-id="96e1a-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="96e1a-108">將 CLR 物件寫入 HTTP 訊息本文</span><span class="sxs-lookup"><span data-stu-id="96e1a-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="96e1a-109">Web API 為 JSON 和 XML 提供媒體類型。</span><span class="sxs-lookup"><span data-stu-id="96e1a-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="96e1a-110">默認情況下,框架將這些處理件插入到管道中。</span><span class="sxs-lookup"><span data-stu-id="96e1a-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="96e1a-111">用戶端可以在 HTTP 請求的「接受」標頭中請求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="96e1a-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="96e1a-112">內容</span><span class="sxs-lookup"><span data-stu-id="96e1a-112">Contents</span></span>

- [<span data-ttu-id="96e1a-113">JSON 媒體類型</span><span class="sxs-lookup"><span data-stu-id="96e1a-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="96e1a-114">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="96e1a-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="96e1a-115">日期</span><span class="sxs-lookup"><span data-stu-id="96e1a-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="96e1a-116">縮排</span><span class="sxs-lookup"><span data-stu-id="96e1a-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="96e1a-117">駱駝外殼</span><span class="sxs-lookup"><span data-stu-id="96e1a-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="96e1a-118">匿名和弱類型物件</span><span class="sxs-lookup"><span data-stu-id="96e1a-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="96e1a-119">XML 媒體類型前物質</span><span class="sxs-lookup"><span data-stu-id="96e1a-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="96e1a-120">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="96e1a-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="96e1a-121">日期</span><span class="sxs-lookup"><span data-stu-id="96e1a-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="96e1a-122">縮排</span><span class="sxs-lookup"><span data-stu-id="96e1a-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="96e1a-123">設定每類型 XML 序列化器</span><span class="sxs-lookup"><span data-stu-id="96e1a-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="96e1a-124">移除 JSON 或 XML 前物質</span><span class="sxs-lookup"><span data-stu-id="96e1a-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="96e1a-125">處理圓形物件參照</span><span class="sxs-lookup"><span data-stu-id="96e1a-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="96e1a-126">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="96e1a-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="96e1a-127">JSON 媒體類型</span><span class="sxs-lookup"><span data-stu-id="96e1a-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="96e1a-128">JSON 格式由**JsonMediaTypeFormatter**類提供。</span><span class="sxs-lookup"><span data-stu-id="96e1a-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="96e1a-129">默認情況下 **,JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)庫執行序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="96e1a-130">Json.NET是第三方開源專案。</span><span class="sxs-lookup"><span data-stu-id="96e1a-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="96e1a-131">如果您願意,可以將**JsonMediaTypeFormatter**類配置為使用**數據合同Jon序列化器**,而不是Json.NET。</span><span class="sxs-lookup"><span data-stu-id="96e1a-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="96e1a-132">此,將**UseDataContractJson 序列化器**屬性設定為**true**:</span><span class="sxs-lookup"><span data-stu-id="96e1a-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="96e1a-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="96e1a-133">JSON Serialization</span></span>

<span data-ttu-id="96e1a-134">本節使用預設[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化器描述 JSON formatter 的一些特定行為。</span><span class="sxs-lookup"><span data-stu-id="96e1a-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="96e1a-135">這不是要全面記錄Json.NET圖書館;有關詳細資訊,請參閱[Json.NET 文檔](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="96e1a-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="96e1a-136">什麼是序列化?</span><span class="sxs-lookup"><span data-stu-id="96e1a-136">What Gets Serialized?</span></span>

<span data-ttu-id="96e1a-137">默認情況下,所有公共屬性和欄位都包含在序列化的 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="96e1a-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="96e1a-138">要省略屬性或欄位,請使用**JsonIgnore**屬性來修飾它。</span><span class="sxs-lookup"><span data-stu-id="96e1a-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="96e1a-139">如果您更喜歡&quot;選擇&quot;加入的方法,請使用**DataContract**屬性修飾類。</span><span class="sxs-lookup"><span data-stu-id="96e1a-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="96e1a-140">如果存在此屬性,則忽略成員,除非它們具有 Data**成員**。</span><span class="sxs-lookup"><span data-stu-id="96e1a-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="96e1a-141">您還可以使用 Data**成員**序列化私有成員。</span><span class="sxs-lookup"><span data-stu-id="96e1a-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="96e1a-142">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="96e1a-142">Read-Only Properties</span></span>

<span data-ttu-id="96e1a-143">預設情況下,唯讀屬性將序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="96e1a-144">日期</span><span class="sxs-lookup"><span data-stu-id="96e1a-144">Dates</span></span>

<span data-ttu-id="96e1a-145">默認情況下,Json.NET以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式寫入日期。</span><span class="sxs-lookup"><span data-stu-id="96e1a-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="96e1a-146">UTC(協調通用時間)中的日期用"Z"後綴書寫。</span><span class="sxs-lookup"><span data-stu-id="96e1a-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="96e1a-147">本地時間中的日期包括時區偏移量。</span><span class="sxs-lookup"><span data-stu-id="96e1a-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="96e1a-148">例如：</span><span class="sxs-lookup"><span data-stu-id="96e1a-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="96e1a-149">默認情況下,Json.NET保留時區。</span><span class="sxs-lookup"><span data-stu-id="96e1a-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="96e1a-150">您可以通過設定 DateTimeZone 處理屬性來覆寫此功能:</span><span class="sxs-lookup"><span data-stu-id="96e1a-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="96e1a-151">如果您更喜歡使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) 而不是 ISO 8601,請使用序列化器設定上設定**DateFormat 處理**屬性:</span><span class="sxs-lookup"><span data-stu-id="96e1a-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="96e1a-152">縮排</span><span class="sxs-lookup"><span data-stu-id="96e1a-152">Indenting</span></span>

<span data-ttu-id="96e1a-153">要編寫縮進的 JSON,請將 **「格式化」** 設定設定為 **「格式化」。**</span><span class="sxs-lookup"><span data-stu-id="96e1a-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="96e1a-154">駱駝外殼</span><span class="sxs-lookup"><span data-stu-id="96e1a-154">Camel Casing</span></span>

<span data-ttu-id="96e1a-155">要使用 camel 大小寫寫入 JSON 屬性名稱,而不變更資料模型,請在序列化器上設定**CamelCasePropertyNames 合同解析器**:</span><span class="sxs-lookup"><span data-stu-id="96e1a-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="96e1a-156">匿名和弱類型物件</span><span class="sxs-lookup"><span data-stu-id="96e1a-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="96e1a-157">操作方法可以返回匿名物件並將其序列化到 JSON。</span><span class="sxs-lookup"><span data-stu-id="96e1a-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="96e1a-158">例如：</span><span class="sxs-lookup"><span data-stu-id="96e1a-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="96e1a-159">回應訊息正文將包含以下 JSON:</span><span class="sxs-lookup"><span data-stu-id="96e1a-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="96e1a-160">如果 Web API 從用戶端接收結構鬆散的 JSON 物件,則可以將請求正文反序列化為**Newtonsoft.Json.Linq.JObject**類型。</span><span class="sxs-lookup"><span data-stu-id="96e1a-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="96e1a-161">但是,通常最好使用強類型數據物件。</span><span class="sxs-lookup"><span data-stu-id="96e1a-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="96e1a-162">然後,您無需自行分析數據,並且得到了模型驗證的好處。</span><span class="sxs-lookup"><span data-stu-id="96e1a-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="96e1a-163">XML 序列化程式不支援匿名類型或**JObject**實例。</span><span class="sxs-lookup"><span data-stu-id="96e1a-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="96e1a-164">如果將這些功能用於 JSON 數據,則應從管道中刪除 XML formatter,如本文後面所述。</span><span class="sxs-lookup"><span data-stu-id="96e1a-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="96e1a-165">XML 媒體類型前物質</span><span class="sxs-lookup"><span data-stu-id="96e1a-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="96e1a-166">XML 格式由**XmlMediaTypeFormatter**類提供。</span><span class="sxs-lookup"><span data-stu-id="96e1a-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="96e1a-167">預設情況下 **,XmlMediaTypeFormatter**使用**資料合同序列化器**類執行序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="96e1a-168">如果您願意,可以將**XmlMediaTypeFormatter**設定為使用 Xml**序列化器**而不是**資料列化器**。</span><span class="sxs-lookup"><span data-stu-id="96e1a-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="96e1a-169">此選項, 將**UseXml 序列化器**屬性設定為**true**:</span><span class="sxs-lookup"><span data-stu-id="96e1a-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="96e1a-170">**XmlSerializer**類支援比**DataContract 序列化器**更窄的類型集,但提供了對生成的 XML 的更多控制。</span><span class="sxs-lookup"><span data-stu-id="96e1a-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="96e1a-171">如果需要符合現有的 XML 架構,請考慮使用**Xml 序列化器**。</span><span class="sxs-lookup"><span data-stu-id="96e1a-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="96e1a-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="96e1a-172">XML Serialization</span></span>

<span data-ttu-id="96e1a-173">本節使用預設**的數據合同序列程式**描述 XML 前物的一些特定行為。</span><span class="sxs-lookup"><span data-stu-id="96e1a-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="96e1a-174">預設情況下,資料合同序列化器的操作方式如下:</span><span class="sxs-lookup"><span data-stu-id="96e1a-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="96e1a-175">所有公共讀/寫屬性和欄位都將序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="96e1a-176">要省略屬性或欄位,請使用**IgnoreData成員**屬性來修飾它。</span><span class="sxs-lookup"><span data-stu-id="96e1a-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="96e1a-177">私有成員和保護成員不序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="96e1a-178">唯讀屬性不序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="96e1a-179">(但是,唯讀集合屬性的內容是序列化的。</span><span class="sxs-lookup"><span data-stu-id="96e1a-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="96e1a-180">類和成員名稱在 XML 中寫入,與類聲明中顯示的完全相同。</span><span class="sxs-lookup"><span data-stu-id="96e1a-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="96e1a-181">使用預設的 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="96e1a-181">A default XML namespace is used.</span></span>

<span data-ttu-id="96e1a-182">如果需要對序列化進行更多控制,可以使用**DataContract**屬性修飾類。</span><span class="sxs-lookup"><span data-stu-id="96e1a-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="96e1a-183">當存在此屬性時,類將序列化如下:</span><span class="sxs-lookup"><span data-stu-id="96e1a-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="96e1a-184">&quot;加入加入&quot;方法:默認情況下不序列化屬性和欄位。</span><span class="sxs-lookup"><span data-stu-id="96e1a-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="96e1a-185">要序列化屬性或欄位,請使用**Data成員**屬性來修飾它。</span><span class="sxs-lookup"><span data-stu-id="96e1a-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="96e1a-186">要序列化私有或受保護成員,請使用**Data成員**屬性裝飾它。</span><span class="sxs-lookup"><span data-stu-id="96e1a-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="96e1a-187">唯讀屬性不序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="96e1a-188">要更改類別名稱在 XML 中的顯示方式,在**DataContract**屬性中設定*Name*參數。</span><span class="sxs-lookup"><span data-stu-id="96e1a-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="96e1a-189">要更改成員名稱在 XML 中的顯示方式,在**DataMs 屬性**中設置*Name*參數。</span><span class="sxs-lookup"><span data-stu-id="96e1a-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="96e1a-190">要更改 XML 命名空間,在**DataContract**類中設定*命名空間*參數。</span><span class="sxs-lookup"><span data-stu-id="96e1a-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="96e1a-191">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="96e1a-191">Read-Only Properties</span></span>

<span data-ttu-id="96e1a-192">唯讀屬性不序列化。</span><span class="sxs-lookup"><span data-stu-id="96e1a-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="96e1a-193">如果唯讀屬性具有支援專用欄位,則可以使用**Data"成員屬性**標記私有欄位。</span><span class="sxs-lookup"><span data-stu-id="96e1a-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="96e1a-194">此方法需要類上的**DataContract**屬性。</span><span class="sxs-lookup"><span data-stu-id="96e1a-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="96e1a-195">日期</span><span class="sxs-lookup"><span data-stu-id="96e1a-195">Dates</span></span>

<span data-ttu-id="96e1a-196">日期以 ISO 8601 格式書寫。</span><span class="sxs-lookup"><span data-stu-id="96e1a-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="96e1a-197">例如, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span><span class="sxs-lookup"><span data-stu-id="96e1a-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="96e1a-198">縮排</span><span class="sxs-lookup"><span data-stu-id="96e1a-198">Indenting</span></span>

<span data-ttu-id="96e1a-199">要編寫縮排的 XML,請將**縮進**屬性設定為**true**:</span><span class="sxs-lookup"><span data-stu-id="96e1a-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="96e1a-200">設定每類型 XML 序列化器</span><span class="sxs-lookup"><span data-stu-id="96e1a-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="96e1a-201">您可以為不同的 CLR 類型設定不同的 XML 序列化器。</span><span class="sxs-lookup"><span data-stu-id="96e1a-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="96e1a-202">例如,您可能有一個特定的數據物件,該物件需要**XmlSerializer**來進行向後相容性。</span><span class="sxs-lookup"><span data-stu-id="96e1a-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="96e1a-203">您可以在此物件使用**Xml 序列化器**,並繼續將**資料列序化器用於其他類型的資料的序列化器**。</span><span class="sxs-lookup"><span data-stu-id="96e1a-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="96e1a-204">要指定特定類型設定 XML 序列化器,請呼叫**Set 序列化器**。</span><span class="sxs-lookup"><span data-stu-id="96e1a-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="96e1a-205">您可以指定**Xml 序列化器**或任何派生自**XmlObject 序列化器**的物件。</span><span class="sxs-lookup"><span data-stu-id="96e1a-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="96e1a-206">移除 JSON 或 XML 前物質</span><span class="sxs-lookup"><span data-stu-id="96e1a-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="96e1a-207">如果不想使用,可以從事件清單中刪除 JSON 事件或 XML 前物質。</span><span class="sxs-lookup"><span data-stu-id="96e1a-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="96e1a-208">這樣做的主要原因是:</span><span class="sxs-lookup"><span data-stu-id="96e1a-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="96e1a-209">將 Web API 回應限制為特定媒體類型。</span><span class="sxs-lookup"><span data-stu-id="96e1a-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="96e1a-210">例如,您可能決定僅支援 JSON 回應,並刪除 XML 前一部分。</span><span class="sxs-lookup"><span data-stu-id="96e1a-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="96e1a-211">將預設前物質替換為自定義前物質。</span><span class="sxs-lookup"><span data-stu-id="96e1a-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="96e1a-212">例如,您可以將 JSON 事件替換為您自己的 JSON 事件的自定義實現。</span><span class="sxs-lookup"><span data-stu-id="96e1a-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="96e1a-213">以下代碼演示如何刪除預設的事務。</span><span class="sxs-lookup"><span data-stu-id="96e1a-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="96e1a-214">從在 Global.asax 中定義的**應用程式\_啟動**方法調用此。</span><span class="sxs-lookup"><span data-stu-id="96e1a-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="96e1a-215">處理圓形物件參照</span><span class="sxs-lookup"><span data-stu-id="96e1a-215">Handling Circular Object References</span></span>

<span data-ttu-id="96e1a-216">默認情況下,JSON 和 XML formatters 將所有物件寫入值。</span><span class="sxs-lookup"><span data-stu-id="96e1a-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="96e1a-217">如果兩個屬性引用同一物件,或者如果同一物件在集合中出現兩次,則 formatter 將序列化該物件兩次。</span><span class="sxs-lookup"><span data-stu-id="96e1a-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="96e1a-218">如果物件圖包含週期,則這是一個特殊問題,因為序列化器在檢測到圖形中的迴圈時將引發異常。</span><span class="sxs-lookup"><span data-stu-id="96e1a-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="96e1a-219">請考慮以下物件模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="96e1a-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="96e1a-220">調用此操作將導致 formatter 引發異常,該異常將轉換為用戶端的狀態代碼 500(內部伺服器錯誤)回應。</span><span class="sxs-lookup"><span data-stu-id="96e1a-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="96e1a-221">要在 JSON 中保留物件參考,請將以下代碼加入到 Global.asax 檔案中**的應用程式\_啟動**方法:</span><span class="sxs-lookup"><span data-stu-id="96e1a-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="96e1a-222">現在控制器操作將返回如下所示的 JSON:</span><span class="sxs-lookup"><span data-stu-id="96e1a-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="96e1a-223">請注意,序列化器向這&quot;&quot;兩個物件添加$id屬性。</span><span class="sxs-lookup"><span data-stu-id="96e1a-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="96e1a-224">此外,它檢測 Employ.Department 屬性創建一個迴圈,因此它將值&quot;替換為 物件引用&quot;:{&quot;&quot;$ref :1 }。</span><span class="sxs-lookup"><span data-stu-id="96e1a-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="96e1a-225">物件引用在 JSON 中不是標準引用。</span><span class="sxs-lookup"><span data-stu-id="96e1a-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="96e1a-226">在使用此功能之前,請考慮用戶端是否能夠分析結果。</span><span class="sxs-lookup"><span data-stu-id="96e1a-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="96e1a-227">最好只是從圖形中刪除迴圈。</span><span class="sxs-lookup"><span data-stu-id="96e1a-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="96e1a-228">例如,在此示例中,從「員工」回部門的連結並不真正是必需的。</span><span class="sxs-lookup"><span data-stu-id="96e1a-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="96e1a-229">要在 XML 中保留物件引用,有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="96e1a-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="96e1a-230">更簡單的選項是`[DataContract(IsReference=true)]`添加到模型類。</span><span class="sxs-lookup"><span data-stu-id="96e1a-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="96e1a-231">*IsReference 參數*啟用物件引用。</span><span class="sxs-lookup"><span data-stu-id="96e1a-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="96e1a-232">請記住 **,DataContract**使用序列化加入,因此您還需要向屬性加入**Data 成員**屬性:</span><span class="sxs-lookup"><span data-stu-id="96e1a-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="96e1a-233">現在,前物質將生成類似於以下內容的 XML:</span><span class="sxs-lookup"><span data-stu-id="96e1a-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="96e1a-234">如果要避免模型類的屬性,還有另一個選項:創建新的類型特定的**DataContract 序列化器**實例,並在構造函數中將*保留物件引用*設定為**true。**</span><span class="sxs-lookup"><span data-stu-id="96e1a-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="96e1a-235">然後,將此實例設置為 XML 媒體類型前物質上的每種類型序列化器。</span><span class="sxs-lookup"><span data-stu-id="96e1a-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="96e1a-236">以下程式碼展示如何執行此操作:</span><span class="sxs-lookup"><span data-stu-id="96e1a-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="96e1a-237">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="96e1a-237">Testing Object Serialization</span></span>

<span data-ttu-id="96e1a-238">在設計 Web API 時,測試數據物件如何序列化非常有用。</span><span class="sxs-lookup"><span data-stu-id="96e1a-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="96e1a-239">無需創建控制器或調用控制器操作即可執行此操作。</span><span class="sxs-lookup"><span data-stu-id="96e1a-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
