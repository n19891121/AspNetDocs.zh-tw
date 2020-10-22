---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API 中的 JSON 和 XML 序列化-ASP.NET 4。x
author: MikeWasson
description: 描述 ASP.NET 4.x ASP.NET Web API 中的 JSON 和 XML 格式器。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: e6e02fa1c48e9c5fb8499379508619ddb317ccc9
ms.sourcegitcommit: c62ec20b453cee3249eb894ecd75013b57d078f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2020
ms.locfileid: "92345170"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="20300-103">ASP.NET Web API 中的 JSON 和 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="20300-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="20300-104">由 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="20300-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="20300-105">本文描述 ASP.NET Web API 中的 JSON 和 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="20300-106">在 ASP.NET Web API 中， *媒體類型格式* 器是一個物件，可以：</span><span class="sxs-lookup"><span data-stu-id="20300-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="20300-107">從 HTTP 訊息主體讀取 CLR 物件</span><span class="sxs-lookup"><span data-stu-id="20300-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="20300-108">將 CLR 物件寫入 HTTP 訊息主體</span><span class="sxs-lookup"><span data-stu-id="20300-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="20300-109">Web API 提供適用于 JSON 和 XML 的媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="20300-110">架構預設會將這些格式器插入管線中。</span><span class="sxs-lookup"><span data-stu-id="20300-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="20300-111">用戶端可以在 HTTP 要求的 Accept 標頭中要求 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="20300-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="20300-112">目錄</span><span class="sxs-lookup"><span data-stu-id="20300-112">Contents</span></span>

- [<span data-ttu-id="20300-113">JSON Media-Type 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="20300-114">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="20300-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="20300-115">日期</span><span class="sxs-lookup"><span data-stu-id="20300-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="20300-116">縮排</span><span class="sxs-lookup"><span data-stu-id="20300-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="20300-117">Camel 大小寫</span><span class="sxs-lookup"><span data-stu-id="20300-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="20300-118">匿名和 Weakly-Typed 物件</span><span class="sxs-lookup"><span data-stu-id="20300-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="20300-119">XML Media-Type 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="20300-120">唯讀屬性</span><span class="sxs-lookup"><span data-stu-id="20300-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="20300-121">日期</span><span class="sxs-lookup"><span data-stu-id="20300-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="20300-122">縮排</span><span class="sxs-lookup"><span data-stu-id="20300-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="20300-123">設定 XML 序列化程式 Per-Type</span><span class="sxs-lookup"><span data-stu-id="20300-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="20300-124">移除 JSON 或 XML 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="20300-125">處理迴圈物件參考</span><span class="sxs-lookup"><span data-stu-id="20300-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="20300-126">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="20300-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="20300-127">JSON Media-Type 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="20300-128">JSON 格式是由 **JsonMediaTypeFormatter** 類別所提供。</span><span class="sxs-lookup"><span data-stu-id="20300-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="20300-129">根據預設， **JsonMediaTypeFormatter** 會使用 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 程式庫來執行序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="20300-130">Json.NET 是協力廠商開放原始碼專案。</span><span class="sxs-lookup"><span data-stu-id="20300-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="20300-131">如果您想要的話，可以設定 **JsonMediaTypeFormatter** 類別使用 **DataContractJsonSerializer** 而不是 Json.NET。</span><span class="sxs-lookup"><span data-stu-id="20300-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="20300-132">若要這樣做，請將 **UseDataContractJsonSerializer** 屬性設定為 **true**：</span><span class="sxs-lookup"><span data-stu-id="20300-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="20300-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="20300-133">JSON Serialization</span></span>

<span data-ttu-id="20300-134">本節將使用預設的 [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) 序列化程式來描述 JSON 格式器的某些特定行為。</span><span class="sxs-lookup"><span data-stu-id="20300-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="20300-135">這不是 Json.NET 程式庫的完整檔;如需詳細資訊，請參閱 [Json.NET 檔](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="20300-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="20300-136">會序列化什麼？</span><span class="sxs-lookup"><span data-stu-id="20300-136">What Gets Serialized?</span></span>

<span data-ttu-id="20300-137">依預設，所有公用屬性和欄位都會包含在序列化的 JSON 中。</span><span class="sxs-lookup"><span data-stu-id="20300-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="20300-138">若要省略屬性或欄位，請使用 **JsonIgnore** 屬性加以裝飾。</span><span class="sxs-lookup"><span data-stu-id="20300-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="20300-139">如果您偏好 &quot; 加入宣告的 &quot; 方法，請使用 **DataContract** 屬性來裝飾類別。</span><span class="sxs-lookup"><span data-stu-id="20300-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="20300-140">如果有這個屬性，除非成員具有 **DataMember**，否則會忽略成員。</span><span class="sxs-lookup"><span data-stu-id="20300-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="20300-141">您也可以使用 **DataMember** 來序列化私用成員。</span><span class="sxs-lookup"><span data-stu-id="20300-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="20300-142">Read-Only 屬性</span><span class="sxs-lookup"><span data-stu-id="20300-142">Read-Only Properties</span></span>

<span data-ttu-id="20300-143">依預設會將唯讀屬性序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="20300-144">日期</span><span class="sxs-lookup"><span data-stu-id="20300-144">Dates</span></span>

<span data-ttu-id="20300-145">根據預設，Json.NET 會以 [ISO 8601](http://www.w3.org/TR/NOTE-datetime) 格式寫入日期。</span><span class="sxs-lookup"><span data-stu-id="20300-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="20300-146">UTC (的日期國際標準時間) 是以 "Z" 尾碼撰寫。</span><span class="sxs-lookup"><span data-stu-id="20300-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="20300-147">當地時間的日期包含時區時差。</span><span class="sxs-lookup"><span data-stu-id="20300-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="20300-148">例如：</span><span class="sxs-lookup"><span data-stu-id="20300-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="20300-149">依預設，Json.NET 會保留時區。</span><span class="sxs-lookup"><span data-stu-id="20300-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="20300-150">您可以藉由設定 DateTimeZoneHandling 屬性來覆寫此屬性：</span><span class="sxs-lookup"><span data-stu-id="20300-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="20300-151">如果您想要使用 [MICROSOFT JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) 而不是 ISO 8601，請在序列化程式設定上設定 **DateFormatHandling** 屬性：</span><span class="sxs-lookup"><span data-stu-id="20300-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="20300-152">縮排</span><span class="sxs-lookup"><span data-stu-id="20300-152">Indenting</span></span>

<span data-ttu-id="20300-153">若要寫入縮排的 JSON，請將 **格式化** 設定設為 **格式化。縮排**：</span><span class="sxs-lookup"><span data-stu-id="20300-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="20300-154">Camel 大小寫</span><span class="sxs-lookup"><span data-stu-id="20300-154">Camel Casing</span></span>

<span data-ttu-id="20300-155">若要使用 camel 大小寫來撰寫 JSON 屬性名稱，而不變更您的資料模型，請在序列化程式上設定 **CamelCasePropertyNamesContractResolver** ：</span><span class="sxs-lookup"><span data-stu-id="20300-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="20300-156">匿名和 Weakly-Typed 物件</span><span class="sxs-lookup"><span data-stu-id="20300-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="20300-157">動作方法可以傳回匿名物件，並將其序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="20300-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="20300-158">例如：</span><span class="sxs-lookup"><span data-stu-id="20300-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="20300-159">回應訊息本文將包含下列 JSON：</span><span class="sxs-lookup"><span data-stu-id="20300-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="20300-160">如果您的 web API 從用戶端接收鬆散結構化的 JSON 物件，您可以將要求本文還原序列化為 \*\* 上的Newtonsoft.Js。JObject\*\* 型別。</span><span class="sxs-lookup"><span data-stu-id="20300-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="20300-161">不過，通常最好使用強型別資料物件。</span><span class="sxs-lookup"><span data-stu-id="20300-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="20300-162">然後您不需要自行剖析資料，並獲得模型驗證的優點。</span><span class="sxs-lookup"><span data-stu-id="20300-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="20300-163">XML 序列化程式不支援匿名型別或 **JObject** 實例。</span><span class="sxs-lookup"><span data-stu-id="20300-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="20300-164">如果您針對 JSON 資料使用這些功能，您應該從管線中移除 XML 格式器，如本文稍後所述。</span><span class="sxs-lookup"><span data-stu-id="20300-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="20300-165">XML Media-Type 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="20300-166">XML 格式是由 **XmlMediaTypeFormatter** 類別所提供。</span><span class="sxs-lookup"><span data-stu-id="20300-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="20300-167">根據預設， **XmlMediaTypeFormatter** 會使用 **DataContractSerializer** 類別來執行序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="20300-168">如果您想要的話，可以將 **XmlMediaTypeFormatter** 設定為使用 **XmlSerializer** ，而不是 **DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="20300-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="20300-169">若要這樣做，請將 **UseXmlSerializer** 屬性設定為 **true**：</span><span class="sxs-lookup"><span data-stu-id="20300-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="20300-170">**XmlSerializer**類別支援比**DataContractSerializer**更窄的型別集，但可讓您更充分掌控所產生的 XML。</span><span class="sxs-lookup"><span data-stu-id="20300-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="20300-171">如果您需要符合現有的 XML 架構，請考慮使用 **XmlSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="20300-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="20300-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="20300-172">XML Serialization</span></span>

<span data-ttu-id="20300-173">本節使用預設 **DataContractSerializer**來描述 XML 格式器的某些特定行為。</span><span class="sxs-lookup"><span data-stu-id="20300-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="20300-174">根據預設，DataContractSerializer 的行為如下：</span><span class="sxs-lookup"><span data-stu-id="20300-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="20300-175">所有公用讀取/寫入屬性和欄位都會進行序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="20300-176">若要省略屬性或欄位，請使用 **IgnoreDataMember** 屬性加以裝飾。</span><span class="sxs-lookup"><span data-stu-id="20300-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="20300-177">私用和受保護成員未序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="20300-178">唯讀屬性未序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="20300-179">不過 (，唯讀集合屬性的內容會被序列化。 ) </span><span class="sxs-lookup"><span data-stu-id="20300-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="20300-180">類別和成員名稱的寫入方式與在類別宣告中所顯示的完全相同。</span><span class="sxs-lookup"><span data-stu-id="20300-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="20300-181">使用預設的 XML 命名空間。</span><span class="sxs-lookup"><span data-stu-id="20300-181">A default XML namespace is used.</span></span>

<span data-ttu-id="20300-182">如果您需要更多的序列化控制權，您可以使用 **DataContract** 屬性裝飾類別。</span><span class="sxs-lookup"><span data-stu-id="20300-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="20300-183">當這個屬性存在時，類別會序列化，如下所示：</span><span class="sxs-lookup"><span data-stu-id="20300-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="20300-184">&quot;選擇 &quot; 使用方法：預設不會序列化屬性和欄位。</span><span class="sxs-lookup"><span data-stu-id="20300-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="20300-185">若要序列化屬性或欄位，請使用 **DataMember** 屬性加以裝飾。</span><span class="sxs-lookup"><span data-stu-id="20300-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="20300-186">若要序列化私用或受保護的成員，請使用 **DataMember** 屬性裝飾。</span><span class="sxs-lookup"><span data-stu-id="20300-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="20300-187">唯讀屬性未序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="20300-188">若要變更類別名稱在 XML 中的顯示方式，請在**DataContract**屬性中設定*name*參數。</span><span class="sxs-lookup"><span data-stu-id="20300-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="20300-189">若要變更成員名稱在 XML 中的顯示方式，請在**DataMember**屬性中設定*name*參數。</span><span class="sxs-lookup"><span data-stu-id="20300-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="20300-190">若要變更 XML 命名空間，請在**DataContract**類別中設定*namespace*參數。</span><span class="sxs-lookup"><span data-stu-id="20300-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="20300-191">Read-Only 屬性</span><span class="sxs-lookup"><span data-stu-id="20300-191">Read-Only Properties</span></span>

<span data-ttu-id="20300-192">唯讀屬性未序列化。</span><span class="sxs-lookup"><span data-stu-id="20300-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="20300-193">如果唯讀屬性具有支援私用欄位，您可以使用 **DataMember** 屬性來標記私用欄位。</span><span class="sxs-lookup"><span data-stu-id="20300-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="20300-194">這種方法需要類別上的 **DataContract** 屬性。</span><span class="sxs-lookup"><span data-stu-id="20300-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="20300-195">日期</span><span class="sxs-lookup"><span data-stu-id="20300-195">Dates</span></span>

<span data-ttu-id="20300-196">日期的寫入格式為 ISO 8601。</span><span class="sxs-lookup"><span data-stu-id="20300-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="20300-197">例如， &quot; 2012-05-23T20：21： 37.9116538 z &quot; 。</span><span class="sxs-lookup"><span data-stu-id="20300-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="20300-198">縮排</span><span class="sxs-lookup"><span data-stu-id="20300-198">Indenting</span></span>

<span data-ttu-id="20300-199">若要寫入縮排的 XML，請將 [ **縮排** ] 屬性設定為 **true**：</span><span class="sxs-lookup"><span data-stu-id="20300-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="20300-200">設定 XML 序列化程式 Per-Type</span><span class="sxs-lookup"><span data-stu-id="20300-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="20300-201">您可以針對不同的 CLR 類型設定不同的 XML 序列化程式。</span><span class="sxs-lookup"><span data-stu-id="20300-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="20300-202">例如，您可能會有特定的資料物件，需要 **XmlSerializer** 以提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="20300-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="20300-203">您可以針對此物件使用 **XmlSerializer** ，並繼續針對其他類型使用 **DataContractSerializer** 。</span><span class="sxs-lookup"><span data-stu-id="20300-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="20300-204">若要設定特定類型的 XML 序列化程式，請呼叫 **SetSerializer**。</span><span class="sxs-lookup"><span data-stu-id="20300-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="20300-205">您可以指定 **XmlSerializer** 或任何衍生自 **XmlObjectSerializer**的物件。</span><span class="sxs-lookup"><span data-stu-id="20300-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="20300-206">移除 JSON 或 XML 格式器</span><span class="sxs-lookup"><span data-stu-id="20300-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="20300-207">如果您不想要使用，您可以從格式器清單中移除 JSON 格式器或 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="20300-208">這樣做的主要原因如下：</span><span class="sxs-lookup"><span data-stu-id="20300-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="20300-209">將您的 web API 回應限制為特定媒體類型。</span><span class="sxs-lookup"><span data-stu-id="20300-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="20300-210">例如，您可能決定僅支援 JSON 回應，並移除 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="20300-211">取代預設格式器與自訂格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="20300-212">例如，您可以使用您自己自訂的 JSON 格式器實作為來取代 JSON 格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="20300-213">下列程式碼顯示如何移除預設格式器。</span><span class="sxs-lookup"><span data-stu-id="20300-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="20300-214">從您的 **應用程式 \_ 啟動** 方法（定義于 global.asax）來呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="20300-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="20300-215">處理迴圈物件參考</span><span class="sxs-lookup"><span data-stu-id="20300-215">Handling Circular Object References</span></span>

<span data-ttu-id="20300-216">根據預設，JSON 和 XML 格式器會以值的形式寫入所有物件。</span><span class="sxs-lookup"><span data-stu-id="20300-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="20300-217">如果兩個屬性參考相同的物件，或者相同的物件出現在集合中兩次，則格式器會將物件序列化兩次。</span><span class="sxs-lookup"><span data-stu-id="20300-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="20300-218">如果您的物件圖形包含迴圈，這是特別的問題，因為當序列化程式在圖形中偵測到迴圈時，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="20300-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="20300-219">請考慮下列物件模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="20300-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="20300-220">叫用此動作將會導致格式器擲回例外狀況，此例外狀況會轉譯為狀態碼 500 (內部伺服器錯誤，) 回應給用戶端。</span><span class="sxs-lookup"><span data-stu-id="20300-220">Invoking this action will cause the formatter to throw an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="20300-221">若要在 JSON 中保留物件參考，請將下列程式碼新增至 global.asax 檔案中的 **應用程式 \_ 啟動** 方法：</span><span class="sxs-lookup"><span data-stu-id="20300-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="20300-222">現在控制器動作會傳回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="20300-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="20300-223">請注意，序列化程式會將 &quot; $id &quot; 屬性加入至這兩個物件。</span><span class="sxs-lookup"><span data-stu-id="20300-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="20300-224">此外，它也會偵測 Employee 屬性會建立迴圈，因此它會將值取代為物件參考： { &quot; $ref &quot; ： &quot; 1 &quot; }。</span><span class="sxs-lookup"><span data-stu-id="20300-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="20300-225">JSON 中的物件參考不是標準。</span><span class="sxs-lookup"><span data-stu-id="20300-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="20300-226">在使用這項功能之前，請考慮您的用戶端是否能夠剖析結果。</span><span class="sxs-lookup"><span data-stu-id="20300-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="20300-227">最好是從圖形中移除迴圈。</span><span class="sxs-lookup"><span data-stu-id="20300-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="20300-228">例如，在此範例中，不需要從員工回到部門的連結。</span><span class="sxs-lookup"><span data-stu-id="20300-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>

<span data-ttu-id="20300-229">若要在 XML 中保留物件參考，您有兩個選項。</span><span class="sxs-lookup"><span data-stu-id="20300-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="20300-230">更簡單的選項是將加入 `[DataContract(IsReference=true)]` 至您的模型類別。</span><span class="sxs-lookup"><span data-stu-id="20300-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="20300-231">*IsReference*參數會啟用物件參考。</span><span class="sxs-lookup"><span data-stu-id="20300-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="20300-232">請記住， **DataContract** 會讓序列化成為加入宣告，因此您也需要將 **DataMember** 屬性新增至屬性：</span><span class="sxs-lookup"><span data-stu-id="20300-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="20300-233">現在格式器會產生類似下面的 XML：</span><span class="sxs-lookup"><span data-stu-id="20300-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="20300-234">如果您想要避免模型類別上的屬性，則有另一個選項：建立新的類型特定 **DataContractSerializer** 實例，並在函式中將 *參見帶有 preserveobjectreferences* 設定為 **true** 。</span><span class="sxs-lookup"><span data-stu-id="20300-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="20300-235">然後，將這個實例設定為 XML 媒體類型格式器上的每一類型序列化程式。</span><span class="sxs-lookup"><span data-stu-id="20300-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="20300-236">下列程式碼示範如何執行這項操作：</span><span class="sxs-lookup"><span data-stu-id="20300-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="20300-237">測試物件序列化</span><span class="sxs-lookup"><span data-stu-id="20300-237">Testing Object Serialization</span></span>

<span data-ttu-id="20300-238">當您設計 web API 時，測試資料物件的序列化方式會很有用。</span><span class="sxs-lookup"><span data-stu-id="20300-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="20300-239">您可以在不建立控制器或叫用控制器動作的情況下執行此動作。</span><span class="sxs-lookup"><span data-stu-id="20300-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
