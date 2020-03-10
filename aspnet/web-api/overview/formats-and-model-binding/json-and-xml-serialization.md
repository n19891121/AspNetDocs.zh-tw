---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API 中的 JSON 和 XML 序列化-ASP.NET 4。x
author: MikeWasson
description: 描述 ASP.NET 4.x 的 ASP.NET Web API 中的 JSON 和 XML 格式器。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557467"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API 中的 JSON 和 XML 序列化

由[Mike Wasson](https://github.com/MikeWasson)

本文說明 ASP.NET Web API 中的 JSON 和 XML 格式器。

在 ASP.NET Web API 中，*媒體類型格式*器是一個物件，可以：

- 從 HTTP 訊息內文讀取 CLR 物件
- 將 CLR 物件寫入 HTTP 訊息內文

Web API 提供適用于 JSON 和 XML 的媒體類型格式器。 根據預設，架構會將這些格式器插入管線中。 用戶端可以在 HTTP 要求的 Accept 標頭中要求 JSON 或 XML。

## <a name="contents"></a>內容

- [JSON 媒體類型格式器](#json_media_type_formatter)

    - [唯讀屬性](#json_readonly)
    - [時間](#json_dates)
    - [進來](#json_indenting)
    - [Camel 大小寫](#json_camelcasing)
    - [匿名和弱式類型物件](#json_anon)
- [XML 媒體類型格式器](#xml_media_type_formatter)

    - [唯讀屬性](#xml_readonly)
    - [時間](#xml_dates)
    - [進來](#xml_indenting)
    - [設定每一類型的 XML 序列化程式](#xml_pertype)
- [移除 JSON 或 XML 格式器](#removing_the_json_or_xml_formatter)
- [處理迴圈物件參考](#handling_circular_object_references)
- [測試物件序列化](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON 媒體類型格式器

JSON 格式是由**JsonMediaTypeFormatter**類別所提供。 根據預設， **JsonMediaTypeFormatter**會使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)程式庫來執行序列化。 Json.NET 是協力廠商的開放原始碼專案。

如果您想要的話，可以將**JsonMediaTypeFormatter**類別設定為使用**DataContractJsonSerializer** ，而不是 Json.NET。 若要這麼做，請將**UseDataContractJsonSerializer**屬性設定為**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON 序列化

本節說明 JSON 格式器的某些特定行為，並使用預設的[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化程式。 這不是 Json.NET 程式庫的完整檔，如需詳細資訊，請參閱[Json.NET 檔](http://james.newtonking.com/projects/json/help/)。

#### <a name="what-gets-serialized"></a>會序列化哪些專案？

根據預設，所有公用屬性和欄位都包含在序列化 JSON 中。 若要省略屬性或欄位，請使用**JsonIgnore**屬性加以裝飾。

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

如果您偏好 &quot;加入宣告&quot; 方法，請使用**DataContract**屬性來裝飾類別。 如果有這個屬性，除非成員具有**DataMember**，否則會忽略它們。 您也可以使用**DataMember**來序列化私用成員。

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>唯讀屬性

預設會序列化唯讀屬性。

<a id="json_dates"></a>
### <a name="dates"></a>日期

根據預設，Json.NET 會以[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式寫入日期。 UTC 格式的日期（國際標準時間）是以 "Z" 後置字元撰寫。 當地時間的日期包含一個時區時差。 例如:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

根據預設，Json.NET 會保留時區。 您可以藉由設定 DateTimeZoneHandling 屬性來覆寫此值：

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

如果您想要使用[MICROSOFT JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)（`"\/Date(ticks)\/"`），而不是 ISO 8601，請設定序列化程式設定上的**DateFormatHandling**屬性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>縮排

若要寫入縮排的 JSON，請將**格式**設定設定為 [**格式化]。縮排**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Camel 大小寫

若要以 camel 大小寫來撰寫 JSON 屬性名稱，而不變更您的資料模型，請在序列化程式上設定**CamelCasePropertyNamesContractResolver** ：

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>匿名和弱式類型物件

動作方法可以傳回匿名物件，並將它序列化為 JSON。 例如:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

回應訊息主體會包含下列 JSON：

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

如果您的 Web API 從用戶端接收鬆散結構化的 JSON 物件，您可以將要求主體還原序列化為**Newtonsoft**類型。

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

不過，使用強型別資料物件通常是比較好的做法。 然後您不需要自行剖析資料，並獲得模型驗證的優點。

XML 序列化程式不支援匿名型別或**JObject**實例。 如果您針對 JSON 資料使用這些功能，您應該從管線中移除 XML 格式器，如本文稍後所述。

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML 媒體類型格式器

XML 格式是由**XmlMediaTypeFormatter**類別所提供。 根據預設， **XmlMediaTypeFormatter**會使用**DataContractSerializer**類別來執行序列化。

如果您想要的話，可以將**XmlMediaTypeFormatter**設定為使用**XmlSerializer** ，而不是**DataContractSerializer**。 若要這麼做，請將**UseXmlSerializer**屬性設定為**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer**類別支援比**DataContractSerializer**更窄的類型集合，但對產生的 XML 提供更多的控制權。 如果您需要符合現有的 XML 架構，請考慮使用**XmlSerializer** 。

### <a name="xml-serialization"></a>XML 序列化

本節使用預設**DataContractSerializer**來描述 XML 格式器的某些特定行為。

根據預設，DataContractSerializer 的行為如下所示：

- 所有公用讀取/寫入屬性和欄位都會進行序列化。 若要省略屬性或欄位，請使用**IgnoreDataMember**屬性加以裝飾。
- 私用和受保護成員不會序列化。
- 唯讀屬性不會序列化。 （不過，唯讀集合屬性的內容會序列化）。
- 類別和成員名稱會以 XML 中的形式，與在類別宣告中所顯示的內容完全相同。
- 會使用預設的 XML 命名空間。

如果您需要更充分掌控序列化，您可以使用**DataContract**屬性來裝飾類別。 當這個屬性存在時，類別會序列化如下：

- &quot;加入宣告&quot; 方法：預設不會序列化屬性和欄位。 若要序列化屬性或欄位，請使用**DataMember**屬性來裝飾它。
- 若要序列化私用或受保護的成員，請使用**DataMember**屬性來裝飾它。
- 唯讀屬性不會序列化。
- 若要變更類別名稱在 XML 中的顯示方式，請在**DataContract**屬性中設定*name*參數。
- 若要變更成員名稱在 XML 中的顯示方式，請在**DataMember**屬性中設定*name*參數。
- 若要變更 XML 命名空間，請在**DataContract**類別中設定*namespace*參數。

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>唯讀屬性

唯讀屬性不會序列化。 如果唯讀屬性具有支援的私用欄位，您可以使用**DataMember**屬性來標記私用欄位。 這個方法需要類別上的**DataContract**屬性。

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>日期

日期是以 ISO 8601 格式撰寫。 例如，&quot;2012-05-23T20：21： 37.9116538 Z&quot;。

<a id="xml_indenting"></a>
### <a name="indenting"></a>縮排

若要寫入縮排的 XML，請將 [**縮排**] 屬性設定為**true**：

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>設定每一類型的 XML 序列化程式

您可以針對不同的 CLR 類型設定不同的 XML 序列化程式。 例如，您可能有需要**XmlSerializer**以提供回溯相容性的特定資料物件。 您可以針對此物件使用**XmlSerializer** ，並繼續使用其他類型的**DataContractSerializer** 。

若要設定特定類型的 XML 序列化程式，請呼叫**SetSerializer**。

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

您可以指定**XmlSerializer**或任何衍生自**XmlObjectSerializer**的物件。

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>移除 JSON 或 XML 格式器

如果您不想要使用，您可以從格式器清單中移除 JSON 格式器或 XML 格式器。 執行此動作的主要原因包括：

- 將您的 Web API 回應限制為特定的媒體類型。 例如，您可能會決定僅支援 JSON 回應，並移除 XML 格式器。
- 以自訂格式器取代預設格式器。 例如，您可以使用 JSON 格式器的自訂執行來取代 JSON 格式器。

下列程式碼顯示如何移除預設的格式器。 從您的應用程式呼叫此項， **\_啟動**方法（定義于 global.asax 中）。

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>處理迴圈物件參考

根據預設，JSON 和 XML 格式器會將所有物件寫入為值。 如果兩個屬性都參考相同的物件，或如果相同的物件在集合中出現兩次，則格式器會將物件序列化兩次。 如果您的物件圖形包含迴圈，這是一個特別的問題，因為當序列化程式在圖形中偵測到迴圈時，將會擲回例外狀況。

請考慮下列物件模型和控制器。

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

叫用此動作會導致格式器擲回例外狀況，這會轉譯為用戶端的狀態碼500（內部伺服器錯誤）回應。

若要保留 JSON 中的物件參考，請將下列程式碼新增至 global.asax 檔案中的**Application\_Start**方法：

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

現在控制器動作會傳回 JSON，如下所示：

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

請注意，序列化程式會將 &quot;$id&quot; 屬性新增至這兩個物件。 此外，它會偵測 Employee. 部門屬性會建立迴圈，因此它會將值取代為物件參考： {&quot;$ref&quot;：&quot;1&quot;}。

> [!NOTE]
> 物件參考在 JSON 中不是標準。 使用這項功能之前，請考慮您的用戶端是否能夠剖析結果。 最好是從圖表中移除迴圈。 例如，在此範例中，從員工到部門的連結並不是真的必要的。

若要在 XML 中保留物件參考，您有兩個選項。 較簡單的選項是將 `[DataContract(IsReference=true)]` 新增至您的模型類別。 *IsReference*參數會啟用物件參考。 請記住， **DataContract**會加入宣告序列化，因此您也需要將**DataMember**屬性新增至屬性：

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

現在，格式器會產生類似下列的 XML：

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

如果您想要避免模型類別上的屬性，還有另一個選項：建立新的類型特定**DataContractSerializer**實例，並在此函式中將*帶有 preserveobjectreferences*設定為**true** 。 然後，將此實例設定為 XML 媒體類型格式器上的每個類型序列化程式。 下列程式碼示範如何執行這項操作：

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>測試物件序列化

當您設計 Web API 時，測試資料物件的序列化方式會很有説明。 您不需要建立控制器或叫用控制器動作，就可以這樣做。

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
