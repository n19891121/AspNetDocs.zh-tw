---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: '瞭解模型、視圖和控制器 (c # ) |Microsoft Docs'
author: StephenWalther
description: 對模型、視圖和控制器有混淆嗎？ 在本教學課程中，Stephen Walther 將為您介紹 ASP.NET MVC 應用程式的不同部分。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: f4d069ddf30634dd6d632468d8e282bf5b2593d3
ms.sourcegitcommit: 4e6d586faadbe4d9ef27122f86335ec9385134af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89045217"
---
# <a name="understanding-models-views-and-controllers-c"></a>了解模型、檢視和控制器 (C#)

依 [Stephen Walther](https://github.com/StephenWalther)

> 對模型、視圖和控制器有混淆嗎？ 在本教學課程中，Stephen Walther 將為您介紹 ASP.NET MVC 應用程式的不同部分。

本教學課程提供 ASP.NET MVC 模型、視圖和控制器的概要說明。 換句話說，它會說明 ASP.NET MVC 中的 M '、V ' 和 C '。

閱讀本教學課程之後，您應該瞭解 ASP.NET MVC 應用程式的不同部分如何一起運作。 您也應該瞭解 ASP.NET MVC 應用程式架構與 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式的差異。

## <a name="the-sample-aspnet-mvc-application"></a>範例 ASP.NET MVC 應用程式

建立 ASP.NET MVC Web 應用程式的預設 Visual Studio 範本包含一個非常簡單的範例應用程式，可用來瞭解 ASP.NET MVC 應用程式的不同部分。 在本教學課程中，我們會利用這個簡單的應用程式。

您可以藉由啟動 Visual Studio 2008 並選取功能表選項 [檔案]、[新增專案] (來建立包含 MVC 範本的新 ASP.NET MVC 應用程式，請參閱 [圖 1]) 。 在 [新增專案] 對話方塊中，從 [專案類型] 下選取您慣用的程式語言 (Visual Basic 或 c # ) 然後選取 [範本] 底下的 [ **ASP.NET MVC Web 應用程式** ] 按一下 [確定] 按鈕。

[![[新增專案] 對話方塊](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)

**圖 01**： [新增專案] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image2.png)) 

當您建立新的 ASP.NET MVC 應用程式時，會出現 [ **建立單元測試專案** ] 對話方塊 (請參閱 [圖 2]) 。 此對話方塊可讓您在方案中建立個別的專案，以測試您的 ASP.NET MVC 應用程式。 選取選項 [ **否，不要建立單元測試專案** ]，然後按一下 [ **確定]** 按鈕。

[![[建立單元測試] 對話方塊](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)

**圖 02**： [建立單元測試] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image4.png)) 

建立新的 ASP.NET MVC 應用程式之後。 在 [方案總管] 視窗中，您會看到數個資料夾和檔案。 特別是，您會看到三個名為「模型」、「Views」和「控制器」的資料夾。 您可能會猜到資料夾名稱，這些資料夾包含用來執行模型、視圖和控制器的檔案。

如果您展開 [控制器] 資料夾，您應該會看到名為 AccountController.cs 的檔案，以及名為 HomeController.cs 的檔案。 如果您展開 Views 資料夾，您應該會看到三個名為 Account、Home 和 Shared 的子資料夾。 如果您展開 [主資料夾] 資料夾，您將會看到兩個名為 [關於 .aspx 和 default.aspx 的檔案 (請參閱 [圖 3]) 。 這些檔案會組成預設 ASP.NET MVC 範本隨附的範例應用程式。

[![方案總管視窗](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)

**圖 03**：方案總管視窗 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image6.png)) 

您可以藉由選取 [偵錯工具]、[ **開始調試**] 來執行範例應用程式。 或者，您也可以按 F5 鍵。

當您第一次執行 ASP.NET 應用程式時，[圖 4] 中的對話方塊會出現，建議您啟用 [偵錯工具] 模式。 按一下 [確定] 按鈕，應用程式就會執行。

[![未啟用 [調試] 對話方塊](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)

**圖 04**：未啟用 [調試] 對話方塊 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image8.png)) 

當您執行 ASP.NET MVC 應用程式時，Visual Studio 會在網頁瀏覽器中啟動應用程式。 範例應用程式只包含兩個頁面： [索引] 頁面和 [關於] 頁面。 當應用程式第一次啟動時，會出現 [索引] 頁面 (請參閱 [圖 5]) 。 您可以按一下應用程式右上方的功能表連結，以流覽至 [關於] 頁面。

[![索引頁面](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)

**圖 05**： [索引] 頁面 ([按一下以查看完整大小的影像](understanding-models-views-and-controllers-cs/_static/image11.png)) 

請注意瀏覽器位址列中的 Url。 例如，當您按一下 [關於] 功能表連結時，瀏覽器位址列中的 URL 會變更為 [ **/Home/About**]。

如果您關閉瀏覽器視窗，並返回 Visual Studio，您將無法找到路徑為 Home/About 的檔案。 檔案不存在。 這有何可能？

## <a name="a-url-does-not-equal-a-page"></a>URL 不等於頁面

當您建立傳統的 ASP.NET Web Forms 應用程式或 Active Server Pages 應用程式時，URL 與頁面之間會有一對一的對應關係。 如果您從伺服器要求名為 SomePage 的頁面，則磁片上的頁面會是名為 SomePage .aspx。 如果 SomePage .aspx 檔案不存在，則會出現不美觀的 **404-找不到頁面** 錯誤。

相較之下，建立 ASP.NET MVC 應用程式時，您在瀏覽器的網址列中輸入的 URL 與您在應用程式中找到的檔案之間並沒有任何對應關係。 在 ASP.NET MVC 應用程式中，URL 會對應至控制器動作，而不是磁片上的頁面。

在傳統的 ASP.NET 或 ASP 應用程式中，瀏覽器要求會對應到頁面。 相反地，在 ASP.NET MVC 應用程式中，瀏覽器要求會對應至控制器動作。 以內容為主的 ASP.NET Web Forms 應用程式。 相反地，ASP.NET MVC 應用程式是以應用程式邏輯為主。

## <a name="understanding-aspnet-routing"></a>瞭解 ASP.NET 路由

瀏覽器要求會透過稱為 *ASP.NET 路由*的 ASP.NET 架構功能，對應至控制器動作。 ASP.NET MVC framework 會使用 ASP.NET 路由將連入要求 *路由傳送* 至控制器動作。

ASP.NET 路由會使用路由表來處理連入要求。 當您的 web 應用程式第一次啟動時，就會建立此路由表。 路由表是在 global.asax 檔案中設定。 預設 MVC global.asax 檔案包含在 [清單 1] 中。

**清單 1-global.asax**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

ASP.NET 應用程式第一次啟動時， \_ 會呼叫應用程式啟動 ( # A1 方法。 在 [清單 1] 中，這個方法會呼叫 RegisterRoutes ( # A1 方法，而 RegisterRoutes ( # A3 方法會建立預設路由表。

預設路由表包含一個路由。 此預設路由會將所有傳入要求分成三個區段， (URL 區段是正斜線) 之間的任何一項。 第一個區段對應到控制器名稱，第二個區段對應至動作名稱，而最後一個區段對應至傳遞給名為 Id 之動作的參數。

例如，請考慮下列 URL：

/Product/Details/3

此 URL 會剖析成三個參數，如下所示：

控制器 = 產品

動作 = 詳細資料

識別碼 = 3

Global.asax 檔案中定義的預設路由包含所有三個參數的預設值。 預設控制器為 [首頁]，預設動作是 [索引]，而預設識別碼為空白字串。 記住這些預設值後，請考慮下列 URL 的剖析方式：

/Employee

此 URL 會剖析成三個參數，如下所示：

控制器 = 員工

Action = Index

識別碼 =

最後，如果您開啟 ASP.NET MVC 應用程式，但未提供任何 URL (例如， `http://localhost`) 則會剖析 URL，如下所示：

控制器 = 首頁

Action = Index

識別碼 =

要求會路由傳送至 HomeController 類別上的索引 ( # A1 動作。

## <a name="understanding-controllers"></a>瞭解控制器

控制器負責控制使用者與 MVC 應用程式互動的方式。 控制器包含 ASP.NET MVC 應用程式的流程式控制制邏輯。 控制器會決定當使用者提出瀏覽器要求時，要傳回給使用者的回應。

控制器只是一個類別 (例如 Visual Basic 或 c # 類別) 。 範例 ASP.NET MVC 應用程式包含一個名為 HomeController.cs 的控制器，位於 [控制器] 資料夾中。 HomeController.cs 檔案的內容會在 [清單 2] 中重現。

**清單 2-HomeController.cs**

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

請注意，HomeController 有兩個名為 Index ( # A1 和 ( # A3 的方法。 這兩個方法會對應至控制器所公開的兩個動作。 URL/Home/Index 會叫用 HomeController， ( # A1 方法，而 URL/Home/About 會叫用 HomeController。關於 ( # A3 方法。

控制器中的任何公用方法都會公開為控制器動作。 您需要特別注意這一點。 這表示任何可存取網際網路的人都可以叫用包含在該控制器中的所有公用方法，方法是在瀏覽器中輸入正確的 URL。

## <a name="understanding-views"></a>了解檢視

HomeController 類別所公開的兩個控制器動作（Index ( # A1 和 ( # A3）會傳回一個 view。 視圖包含 HTML 標籤和傳送至瀏覽器的內容。 View 相當於使用 ASP.NET MVC 應用程式時的頁面。

您必須在正確的位置建立您的視圖。 HomeController ( # A1 動作會傳回位於下列路徑的視圖：

\Views\Home\Index.aspx

HomeController. About ( # A1 動作會傳回位於下列路徑的視圖：

\Views\Home\About.aspx

一般情況下，如果您想要傳回控制器動作的視圖，則需要在 [Views] 資料夾中建立與控制器相同名稱的子資料夾。 在子資料夾內，您必須建立與控制器動作相同名稱的 .aspx 檔案。

[清單 3] 中的檔案包含有關 .aspx 的觀點。

**清單 3-關於 .aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

如果您忽略 [清單 3] 中的第一行，則大部分的視圖都是由標準 HTML 組成。 您可以在這裡輸入任何您想要的 HTML 來修改視圖的內容。

View 與 Active Server Pages 或 ASP.NET Web Forms 中的頁面非常類似。 一個視圖可以包含 HTML 內容和腳本。 您可以用您最愛的 .NET 程式設計語言撰寫腳本 (例如，c # 或 Visual Basic .NET) 。 您可以使用腳本來顯示動態內容，例如資料庫資料。

## <a name="understanding-models"></a>瞭解模型

我們已討論過控制器，並已討論過這些觀點。 我們必須討論的最後一個主題是模型。 什麼是 MVC 模型？

MVC 模型包含所有不包含在視圖或控制器中的應用程式邏輯。 此模型應該包含您所有的應用程式商務邏輯、驗證邏輯和資料庫存取邏輯。 例如，如果您使用 Microsoft Entity Framework 來存取資料庫，則您會在 [模型] 資料夾中) 您的 .edmx 檔案 (建立 Entity Framework 類別。

視圖應該只包含與產生使用者介面相關的邏輯。 控制器應該只包含傳回右視圖所需的最低邏輯，或將使用者重新導向至另一個動作 (流量控制) 。 其他所有專案都應該包含在模型中。

一般情況下，您應該努力進行 fat 模型和訣竅控制器。 您的控制器方法應該只包含幾行程式碼。 如果控制器動作變得太長，您應該考慮將邏輯移出 [模型] 資料夾中的新類別。

## <a name="summary"></a>摘要

本教學課程提供 ASP.NET MVC web 應用程式中不同部分的概要總覽。 您已瞭解 ASP.NET 路由如何將連入瀏覽器要求對應至特定的控制器動作。 您已瞭解控制器如何協調將視圖傳回至瀏覽器的方式。 最後，您已瞭解模型如何包含應用程式的商務、驗證和資料庫存取邏輯。
