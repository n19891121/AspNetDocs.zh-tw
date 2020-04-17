---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和不顯眼的 JavaScript 創建 MVC 3 應用程式 |微軟文件
author: rick-anderson
description: 使用者列表示例 Web 應用程式演示了使用 Razor 檢視引擎創建 ASP.NET MVC 3 應用程式是多麼簡單。 範例應用程式...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: c57e19f8eeca15e3676b3d490b08f69786d44f93
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542452"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>使用 Razor 和低調的 JavaScript 建立 MVC 3 應用程式

由[微軟](https://github.com/microsoft)

> 使用者列表示例 Web 應用程式演示了使用 Razor 檢視引擎創建 ASP.NET MVC 3 應用程式是多麼簡單。 該示例應用程式演示如何使用帶有 ASP.NET mVC 版本 3 和 Visual Studio 2010 的新 Razor 檢視引擎來創建虛構的使用者清單網站,該網站包含創建、顯示、編輯和刪除使用者等功能。
> 
> 本教程介紹為生成使用者列表示例而採取的步驟ASP.NET MVC 3 應用程式。 以 C# 與 VB 原始碼的視覺化工作室項目可隨同本主題:[下載](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。 如果您對本教程有疑問,請將其發佈到[MVC 論壇](https://forums.asp.net/1146.aspx)。

## <a name="overview"></a>總覽

您將建置的應用程式是一個簡單的使用者清單網站。 用戶可以輸入、查看和更新使用者資訊。

![範例網站](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

您可以[在此處](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)下載 VB 和 C# 已完成的專案。

## <a name="creating-the-web-application"></a>建立 Web 應用程式

要開始本教程,請打開 Visual Studio 2010 並使用ASP.NET *MVC 3 Web 應用程式*樣本創建新專案。 命名應用程式&quot;Mvc3Razor&quot;。

[![新的 MVC 3 專案](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

在新**ASP.NET MVC 3 專案**對話方塊中,選擇 Internet**應用程式**,選擇 Razor 檢視引擎,然後單擊「**確定**」。

![新ASP.NET MVC 3 專案對話框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

在本教學中,您將不使用ASP.NET成員資格提供者,因此您可以刪除與登錄和成員資格關聯的所有檔。 在**解決方案資源管理員中**,刪除以下檔案與目錄:

- *控制器\帳戶控制器*
- *模型_帳戶模型*
- *檢視\共用\\_LogOnPartial*
- *檢視\帳號*(以及此目錄中的所有檔案)

![索倫·Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

編輯<em>\_Layout.cshtml</em>檔,`<div>``logindisplay`並將命名 的元素內的標記<em>&quot;</em>替換為消息 「登錄&quot;禁用」。。 下面的範例顯示了新的標記:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>新增模型

在 **「解決方案資源管理員」** 中,右鍵按*下模型模型資料夾*,選擇 **「添加**」,然後按下 **「類**」。

![新使用者 Mdl 類別](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

將類別命名為 `UserModel`。 將*UserModel*檔案的內容取代為以下代碼:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

類`UserModel`表示使用者。 類別每個成員都使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的[「必需」](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性進行註解。 [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的屬性為 Web 應用程式提供自動用戶端和伺服器端驗證。

開啟類別`HomeController`並新增`using`指令 ,以便您可以`UserModel``Users`存取 與類別:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

聲明之後`HomeController`,添加以下註釋和`Users`對 類的引用:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

該`Users`類是一個簡化的記憶體數據存儲,您將在本教程中使用。 在實際應用程式中,您將使用資料庫來存儲使用者資訊。 `HomeController`該檔案的前幾行顯示在以下範例中:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

生成應用程式,以便使用者模型在下一步中可供基架嚮導使用。

## <a name="creating-the-default-view"></a>建立預設檢視

下一步是添加一個操作方法和視圖來顯示使用者。

刪除現有的*檢視\Home_索引*檔。 您將創建新*的 Index*檔以顯示使用者。

在`HomeController`類別中,`Index`將方法的內容取代為以下代碼:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

右鍵按一下方法`Index`內 ,然後按下「**添加檢視**」。

![新增檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

選擇「**創建強類型檢視**」 選項。 對於**查看資料類別**,請選擇**Mvc3Razor.Model.UserModel**。 (如果您沒有看到**Mvc3Razor.Models.UserModel**在 **"查看數據"類**框中,則需要生成專案。確保檢視引擎設定為**Razor**。 將 **「查看內容**」設置為 **「清單**」,然後按下「**添加**」 。

![新增索引檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

新檢視會自動對傳遞給`Index`檢視的用戶數據基腳架。 檢查新生成的*檢視\Home_Index*檔。 **"創建新**"、"**編輯**"、"**詳細資訊**"和 **"刪除**"連結不起作用,但頁面的其餘部分正常工作。 運行頁面。 您將看到使用者清單。

![索引頁](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

開啟*Index.cshtml*檔案`ActionLink`,以以以下代碼取代**編輯**,**請詳細資訊**與**刪除**的標籤:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

使用者名用作 ID,用於在 **「編輯**」、「**詳細資訊****」和「刪除**」連結中尋找所選記錄。

## <a name="creating-the-details-view"></a>建立詳細資訊檢視

下一步是添加操作`Details`方法和視圖,以便顯示使用者詳細資訊。

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

將以下`Details`方法加入主控制器:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

右鍵按一下方法`Details`內 ,然後選擇<strong>「添加檢視</strong>」。。 認證<strong>「檢視資料類別」</strong>框是否包含<strong>Mvc3Razor.Model.UserModel</strong><em>。</em> 將<strong>「查看內容」</strong>設定為<strong>「詳細資訊</strong>」,然後按下「<strong>添加</strong>」。

![新增詳細資訊檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

運行應用程式並選擇詳細資訊連結。 自動基架顯示模型中的每個屬性。

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>建立編輯檢視

將以下`Edit`方法添加到主控制器。

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

添加檢視與前面的步驟一樣,但將 **「查看內容」** 設定為 **「編輯**」。。

![新增編輯檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

運行應用程式並編輯其中一個使用者的名字和姓氏。 如果違反了已應用於`DataAnnotation``UserModel`類的任何約束,則在提交表單時,將看到伺服器代碼生成的驗證錯誤。 例如,如果在提交表單時將名字&quot;Ann&quot; &quot;&quot;更改為 A,則表單上將顯示以下錯誤:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

在本教程中,您將使用者名視為主鍵。 因此,無法更改使用者名屬性。 在*Edit.cshtml*檔中`Html.BeginForm`,在語句之後,將使用者名設置為隱藏欄位。 這將導致在模型中傳遞該屬性。 以下片段顯示敘述的位置`Hidden`:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

將`TextBoxFor`使用者名的`ValidationMessageFor`和標記替換為`DisplayFor`調用。 該方法`DisplayFor`將該屬性顯示為唯讀元素。 下列範例顯示完整的標記。 原始`TextBoxFor``ValidationMessageFor`與呼叫 Razor 開頭註解與結束註解字元`@* *@`() 註解出來

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>開啟客戶端驗證

要在 ASP.NET MVC 3 中啟用客戶端驗證,必須設置兩個標誌,並且必須包含三個 JavaScript 檔。

開啟應用程式的*Web.config*檔案。 在`that ClientValidationEnabled`應用程式`UnobtrusiveJavaScriptEnabled`設定中驗證並設置為 true。 root *Web.config*檔案中的以下片段顯示了正確的設定:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

設置為`UnobtrusiveJavaScriptEnabled`true 可實現不顯眼的 Ajax 和不顯眼的客戶端驗證。 使用不顯眼的驗證時,驗證規則將轉換為 HTML5 屬性。 HTML5 屬性名稱只能包含小寫字母、數位和破折號。

設置為`ClientValidationEnabled`true 啟用客戶端驗證。 通過在應用程式*Web.config 檔中*設定這些金鑰,您可以為整個應用程式啟用客戶端驗證和不顯眼的 JavaScript。 您可以使用以下代碼在單個檢視或控制器方法中啟用或關閉這些設定:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

您還需要在呈現的檢視中包含多個 JavaScript 檔。 在所有檢視中包含 JavaScript 的一種簡單方法是將它們添加到*檢視_\\共用 _Layout.cshtml*檔中。 `<head>`*將\_Layout.cshtml*檔案的元素取代為以下代碼:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

前兩個 jQuery 腳本由 Microsoft Ajax 內容交付網路 (CDN) 託管。 通過利用 Microsoft Ajax CDN,您可以顯著提高應用程式的第一熱性能。

運行應用程式並按一下編輯連結。 在瀏覽器中查看頁面的源。 瀏覽器源顯示表單`data-val`的許多屬性(用於資料驗證)。 啟用客戶端驗證和不顯眼的 JavaScript 時,具有用戶端驗證規則的輸入欄`data-val="true"`位包含該 屬性以觸發不顯眼的客戶端驗證。 例如,模型中的`City`欄位用[「必需」](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性進行修飾,這將導致以下範例中顯示的 HTML:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

對於每個用戶端驗證規則,將添加具有窗體`data-val-rulename="message"`的屬性。 使用前面`City`顯示的欄位範例,所需的用戶端驗證規則將`data-val-required`生成 該屬性,&quot;並且消息「城市」欄位是必需&quot;的。 運行應用程式,編輯其中一個使用者,並清除該`City`欄位。 當您選項卡出欄位時,您將看到客戶端驗證錯誤訊息。

![城市需要](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

同樣,對於用戶端驗證規則中的每個參數,將添加具有窗體`data-val-rulename-paramname=paramvalue`的屬性。 例如,`FirstName`使用[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性對屬性進行批號,並指定最小長度為 3 和最大長度為 8。 命名的`length`資料驗證規則具有參數`max`名稱 和參數值 8。 下面顯示了在編輯其中一個使用者時為`FirstName`字段產生的 HTML:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

有關不顯眼的客戶端驗證的詳細資訊,請參閱 brad Wilson 博客[中ASP.NET MVC 3 中的"不顯眼客戶端驗證](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)"條目。

> [!NOTE]
> 在ASP.NET MVC 3 測試版中,有時需要提交表單才能啟動客戶端驗證。 對於最終版本,可能會更改此情況。

## <a name="creating-the-create-view"></a>建立檢視

下一步是添加操作`Create`方法和視圖,以便使用戶能夠創建新使用者。 將以下`Create`方法加入主控制器:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

添加檢視與前面的步驟一樣,但將 **「檢視內容」** 設定為 **「創建**」。。

![建立檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

運行應用程式,選擇 **「創建**」連結,然後添加新使用者。 該方法`Create`會自動利用用戶端和伺服器端驗證。 嘗試輸入包含空白的使用者名稱,如&quot;Ben&quot;X 。 當您從使用者名稱選項卡外時,將顯示客戶端驗證錯誤 (`White space is not allowed`) 。

## <a name="add-the-delete-method"></a>新增移除方法

要完成本教學,請向主控制器`Delete`添加以下方法:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

新增`Delete`檢視,如前面的步驟,**將"查看內容"** 設定為 **"刪除**"。

![刪除檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

現在,您擁有一個簡單但功能齊全ASP.NET MVC 3 應用程式,並具有驗證功能。
