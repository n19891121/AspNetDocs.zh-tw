---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 將驗證加入至模型 (C#) |Microsoft Docs
author: Rick-Anderson
description: 建立控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: d6ad229775da61544d2d97e75b291d158e79af87
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130135"
---
# <a name="adding-validation-to-the-model-c"></a>將驗證新增至模型 (C#)

藉由[Rick Anderson]((https://twitter.com/RickAndMSFT))

> > [!NOTE]
> > 本教學課程中的更新的版本可[此處](../../../getting-started/introduction/getting-started.md)使用 ASP.NET MVC 5 和 Visual Studio 2013。 它更安全、 更容易遵循，並示範更多的功能。
> 
> 
> 本教學課程將教導您建置使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，也就是 Microsoft Visual Studio 的免費版本的 ASP.NET MVC Web 應用程式的基本概念。 在開始之前，請確定您已安裝符合下列先決條件。 您可以安裝所有人都按下列連結：[Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，您可以個別安裝的必要條件，使用下列連結：
> 
> - [Visual Studio Web Developer Express SP1 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Tools Update](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行階段 + 工具支援）
> 
> 如果您使用 Visual Studio 2010，而不 Visual Web Developer 2010，請按一下下列連結安裝必要條件：[Visual Studio 2010 的必要元件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 使用本主題隨附了 C# 原始程式碼的 Visual Web Developer 專案。 [下載 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您偏好 Visual Basic，切換到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教學課程。

在本節中，您會將驗證邏輯加入`Movie`模型，而您將確保的每當使用者嘗試建立或編輯電影，使用應用程式執行驗證規則。

## <a name="keeping-things-dry"></a>項目保持 DRY

ASP.NET mvc 的核心設計原則之一是 DRY （「 不自行重複 」）。 ASP.NET MVC 鼓勵您一次，指定功能或行為，然後讓它會反映在應用程式中的所有位置。 這可減少您需要撰寫的程式碼數量，並可讓您維護更容易撰寫的程式碼。

ASP.NET MVC 和 Entity Framework Code First 所提供的驗證支援就是執行 DRY 準則的動作的絕佳範例。 您可以以宣告方式指定在單一位置 （在模型類別中） 中的驗證規則，然後這些規則是任何位置強制執行應用程式中。

讓我們看看如何您可以利用這項驗證支援的電影應用程式中。

## <a name="adding-validation-rules-to-the-movie-model"></a>將驗證規則新增至電影模型

一開始要先新增一些驗證邏輯，以`Movie`類別。

開啟 *Movie.cs* 檔案。 新增`using`陳述式參考的檔案頂端[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

命名空間是.NET Framework 的一部分。 它提供一組內建的驗證屬性，您可以以宣告方式套用至任何類別或屬性。

現在更新`Movie`類別，以充分利用內建[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，並[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)驗證屬性. 使用下列程式碼作為範例，要套用屬性的位置。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

驗證屬性會指定您想要強制執行模型屬性套用的行為。 `Required`屬性會指出屬性必須有值; 在此範例中，電影必須具有值`Title`， `ReleaseDate`， `Genre`，和`Price`屬性才會生效。 `Range` 屬性會將值限制在指定的範圍內。 `StringLength` 屬性可讓您設定字串屬性的最大長度，並選擇性設定其最小長度。

程式碼會先確認您的模型類別指定的驗證規則會強制執行，才能應用程式會將變更儲存在資料庫中。 例如，下列程式碼將會擲回例外狀況時`SaveChanges`呼叫方法，因為數個需要`Movie`屬性值遺漏，且價格為零 （這是超出有效範圍）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

具有自動強制執行的.NET Framework 的驗證規則有助於讓您的應用程式更穩固。 它也確保您不會忘記要驗證某些項目，不小心讓不正確的資料進入資料庫。

以下是完整的程式碼，更新清單*Movie.cs*檔案：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>驗證錯誤 ASP.NET MVC 中的 UI

重新執行應用程式，並瀏覽至 */Movies* URL。

按一下 **建立的電影**連結，可新增一部新電影。 填妥表單中使用某些無效的值，然後按一下 [**建立**] 按鈕。

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

請注意如何表單已自動使用背景色彩來反白顯示的文字方塊，其中包含無效的資料，並發出每一個旁適當的驗證錯誤訊息。 錯誤訊息符合您指定當您的註解的錯誤字串`Movie`類別。 錯誤會強制執行 （使用 JavaScript） 用戶端和伺服器端 （如果使用者已停用 JavaScript 時）。

實質的好處是，您不需要變更任何程式中的程式碼`MoviesController`類別或*Create.cshtml*才能啟用這項驗證 UI 的檢視。 控制器和檢視您稍早在本教學課程中自動建立拾取驗證規則，您指定的資料上使用屬性`Movie`模型類別。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何驗證發生在 建立檢視，以及建立動作方法

您可能奇怪如何在不更新控制器或檢視程式碼的狀況下產生驗證 UI。 下一步 的清單顯示什麼`Create`中的方法`MovieController`類別看起來像。 它們與您建立的方式加以稍早在本教學課程中相同。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

第一個動作方法會顯示初始建立表單。 第二個處理表單張貼。 第二個`Create`方法呼叫`ModelState.IsValid`檢查電影是否有任何驗證錯誤。 呼叫此方法會評估已套用至物件的所有驗證屬性。 如果物件有驗證錯誤`Create`方法會重新顯示表單。 如果沒有任何錯誤，方法即會將新的電影儲存到資料庫。

以下是*Create.cshtml*您稍早在本教學課程中包含 scaffold 的檢視範本。 上述動作方法會使用它來顯示初始表單，以及在發生錯誤時重新顯示它。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

請注意程式碼的使用方式`Html.EditorFor`輸出的協助專家`<input>`每個項目`Movie`屬性。 此協助程式旁會呼叫`Html.ValidationMessageFor`helper 方法。 這兩個 helper 方法會使用控制器傳遞至檢視的模型物件 (在此情況下，`Movie`物件)。 它們會自動尋找適當的模型並顯示錯誤訊息中指定的驗證屬性。

什麼是這種方法的優點在於控制器和 Create 檢視範本都不知道的任何項目顯示的特定錯誤訊息或強制執行的實際驗證規則相關。 驗證規則和錯誤字串只在 `Movie` 類別中指定。

如果您想要稍後變更驗證邏輯，則可以只在一個位置。 您不必擔心應用程式的不同部分會與規則強制執行的方式不一致，所有的驗證邏輯都是在同一個地方定義，用於所有位置。 這會讓程式碼非常整齊乾淨，容易維護及發展。 這表示您會完全接受 DRY 原則。

## <a name="adding-formatting-to-the-movie-model"></a>加入至電影模型格式設定

開啟 *Movie.cs* 檔案。 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間會提供除了一組內建的驗證屬性的格式化屬性。 您將會套用[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性並[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)發行日期和價格欄位的列舉值。 下列程式碼示範`ReleaseDate`並`Price`屬性以適當[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)屬性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

或者，您也可以明確設定[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下列程式碼顯示以日期格式字串的發行日期屬性 (也就是"d")。 您會使用此對話方塊來指定您不想要時間發行日期的一部分。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

下列程式碼格式`Price`屬性做為貨幣。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

完整`Movie`類別如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

執行應用程式，並瀏覽至`Movies`控制站。

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

在數列的下一個部分中，我們會檢閱應用程式，並對自動產生的 `Details` 和 `Delete` 方法進行一些改良。

> [!div class="step-by-step"]
> [上一頁](adding-a-new-field.md)
> [下一頁](improving-the-details-and-delete-methods.md)
