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
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API 中的 JSON 和 XML 序列化

由[邁克·瓦森](https://github.com/MikeWasson)

本文介紹了ASP.NET Web API 中的 JSON 和 XML 等事。

在 Web API ASP.NET,*媒體類型的前物質*是一個物件,可以:

- 從 HTTP 訊息正課程讀取 CLR 物件
- 將 CLR 物件寫入 HTTP 訊息本文

Web API 為 JSON 和 XML 提供媒體類型。 默認情況下,框架將這些處理件插入到管道中。 用戶端可以在 HTTP 請求的「接受」標頭中請求 JSON 或 XML。

## <a name="contents"></a>內容

- [JSON 媒體類型](#json_media_type_formatter)

    - [唯讀屬性](#json_readonly)
    - [日期](#json_dates)
    - [縮排](#json_indenting)
    - [駱駝外殼](#json_camelcasing)
    - [匿名和弱類型物件](#json_anon)
- [XML 媒體類型前物質](#xml_media_type_formatter)

    - [唯讀屬性](#xml_readonly)
    - [日期](#xml_dates)
    - [縮排](#xml_indenting)
    - [設定每類型 XML 序列化器](#xml_pertype)
- [移除 JSON 或 XML 前物質](#removing_the_json_or_xml_formatter)
- [處理圓形物件參照](#handling_circular_object_references)
- [測試物件序列化](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON 媒體類型

JSON 格式由**JsonMediaTypeFormatter**類提供。 默認情況下 **,JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)庫執行序列化。 Json.NET是第三方開源專案。

如果您願意,可以將**JsonMediaTypeFormatter**類配置為使用**數據合同Jon序列化器**,而不是Json.NET。 此,將**UseDataContractJson 序列化器**屬性設定為**true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON 序列化

本節使用預設[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化器描述 JSON formatter 的一些特定行為。 這不是要全面記錄Json.NET圖書館;有關詳細資訊,請參閱[Json.NET 文檔](http://james.newtonking.com/projects/json/help/)。

#### <a name="what-gets-serialized"></a>什麼是序列化?

默認情況下,所有公共屬性和欄位都包含在序列化的 JSON 中。 要省略屬性或欄位,請使用**JsonIgnore**屬性來修飾它。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

如果您更喜歡&quot;選擇&quot;加入的方法,請使用**DataContract**屬性修飾類。 如果存在此屬性,則忽略成員,除非它們具有 Data**成員**。 您還可以使用 Data**成員**序列化私有成員。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>唯讀屬性

預設情況下,唯讀屬性將序列化。

<a id="json_dates"></a>
### <a name="dates"></a>日期

默認情況下,Json.NET以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式寫入日期。 UTC(協調通用時間)中的日期用"Z"後綴書寫。 本地時間中的日期包括時區偏移量。 例如：

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

默認情況下,Json.NET保留時區。 您可以通過設定 DateTimeZone 處理屬性來覆寫此功能:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

如果您更喜歡使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) 而不是 ISO 8601,請使用序列化器設定上設定**DateFormat 處理**屬性:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>縮排

要編寫縮進的 JSON,請將 **「格式化」** 設定設定為 **「格式化」。**

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>駱駝外殼

要使用 camel 大小寫寫入 JSON 屬性名稱,而不變更資料模型,請在序列化器上設定**CamelCasePropertyNames 合同解析器**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>匿名和弱類型物件

操作方法可以返回匿名物件並將其序列化到 JSON。 例如：

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

回應訊息正文將包含以下 JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

如果 Web API 從用戶端接收結構鬆散的 JSON 物件,則可以將請求正文反序列化為**Newtonsoft.Json.Linq.JObject**類型。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

但是,通常最好使用強類型數據物件。 然後,您無需自行分析數據,並且得到了模型驗證的好處。

XML 序列化程式不支援匿名類型或**JObject**實例。 如果將這些功能用於 JSON 數據,則應從管道中刪除 XML formatter,如本文後面所述。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML 媒體類型前物質

XML 格式由**XmlMediaTypeFormatter**類提供。 預設情況下 **,XmlMediaTypeFormatter**使用**資料合同序列化器**類執行序列化。

如果您願意,可以將**XmlMediaTypeFormatter**設定為使用 Xml**序列化器**而不是**資料列化器**。 此選項, 將**UseXml 序列化器**屬性設定為**true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer**類支援比**DataContract 序列化器**更窄的類型集,但提供了對生成的 XML 的更多控制。 如果需要符合現有的 XML 架構,請考慮使用**Xml 序列化器**。

### <a name="xml-serialization"></a>XML 序列化

本節使用預設**的數據合同序列程式**描述 XML 前物的一些特定行為。

預設情況下,資料合同序列化器的操作方式如下:

- 所有公共讀/寫屬性和欄位都將序列化。 要省略屬性或欄位,請使用**IgnoreData成員**屬性來修飾它。
- 私有成員和保護成員不序列化。
- 唯讀屬性不序列化。 (但是,唯讀集合屬性的內容是序列化的。
- 類和成員名稱在 XML 中寫入,與類聲明中顯示的完全相同。
- 使用預設的 XML 命名空間。

如果需要對序列化進行更多控制,可以使用**DataContract**屬性修飾類。 當存在此屬性時,類將序列化如下:

- &quot;加入加入&quot;方法:默認情況下不序列化屬性和欄位。 要序列化屬性或欄位,請使用**Data成員**屬性來修飾它。
- 要序列化私有或受保護成員,請使用**Data成員**屬性裝飾它。
- 唯讀屬性不序列化。
- 要更改類別名稱在 XML 中的顯示方式,在**DataContract**屬性中設定*Name*參數。
- 要更改成員名稱在 XML 中的顯示方式,在**DataMs 屬性**中設置*Name*參數。
- 要更改 XML 命名空間,在**DataContract**類中設定*命名空間*參數。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>唯讀屬性

唯讀屬性不序列化。 如果唯讀屬性具有支援專用欄位,則可以使用**Data"成員屬性**標記私有欄位。 此方法需要類上的**DataContract**屬性。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日期

日期以 ISO 8601 格式書寫。 例如, &quot;2012-05-23T20:21:37.9116538Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>縮排

要編寫縮排的 XML,請將**縮進**屬性設定為**true**:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>設定每類型 XML 序列化器

您可以為不同的 CLR 類型設定不同的 XML 序列化器。 例如,您可能有一個特定的數據物件,該物件需要**XmlSerializer**來進行向後相容性。 您可以在此物件使用**Xml 序列化器**,並繼續將**資料列序化器用於其他類型的資料的序列化器**。

要指定特定類型設定 XML 序列化器,請呼叫**Set 序列化器**。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

您可以指定**Xml 序列化器**或任何派生自**XmlObject 序列化器**的物件。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>移除 JSON 或 XML 前物質

如果不想使用,可以從事件清單中刪除 JSON 事件或 XML 前物質。 這樣做的主要原因是:

- 將 Web API 回應限制為特定媒體類型。 例如,您可能決定僅支援 JSON 回應,並刪除 XML 前一部分。
- 將預設前物質替換為自定義前物質。 例如,您可以將 JSON 事件替換為您自己的 JSON 事件的自定義實現。

以下代碼演示如何刪除預設的事務。 從在 Global.asax 中定義的**應用程式\_啟動**方法調用此。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>處理圓形物件參照

默認情況下,JSON 和 XML formatters 將所有物件寫入值。 如果兩個屬性引用同一物件,或者如果同一物件在集合中出現兩次,則 formatter 將序列化該物件兩次。 如果物件圖包含週期,則這是一個特殊問題,因為序列化器在檢測到圖形中的迴圈時將引發異常。

請考慮以下物件模型和控制器。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

調用此操作將導致 formatter 引發異常,該異常將轉換為用戶端的狀態代碼 500(內部伺服器錯誤)回應。

要在 JSON 中保留物件參考,請將以下代碼加入到 Global.asax 檔案中**的應用程式\_啟動**方法:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

現在控制器操作將返回如下所示的 JSON:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

請注意,序列化器向這&quot;&quot;兩個物件添加$id屬性。 此外,它檢測 Employ.Department 屬性創建一個迴圈,因此它將值&quot;替換為 物件引用&quot;:{&quot;&quot;$ref :1 }。

> [!NOTE]
> 物件引用在 JSON 中不是標準引用。 在使用此功能之前,請考慮用戶端是否能夠分析結果。 最好只是從圖形中刪除迴圈。 例如,在此示例中,從「員工」回部門的連結並不真正是必需的。

要在 XML 中保留物件引用,有兩個選項。 更簡單的選項是`[DataContract(IsReference=true)]`添加到模型類。 *IsReference 參數*啟用物件引用。 請記住 **,DataContract**使用序列化加入,因此您還需要向屬性加入**Data 成員**屬性:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

現在,前物質將生成類似於以下內容的 XML:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

如果要避免模型類的屬性,還有另一個選項:創建新的類型特定的**DataContract 序列化器**實例,並在構造函數中將*保留物件引用*設定為**true。** 然後,將此實例設置為 XML 媒體類型前物質上的每種類型序列化器。 以下程式碼展示如何執行此操作:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>測試物件序列化

在設計 Web API 時,測試數據物件如何序列化非常有用。 無需創建控制器或調用控制器操作即可執行此操作。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
