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
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="08e7f-104">使用 Razor 和低調的 JavaScript 建立 MVC 3 應用程式</span><span class="sxs-lookup"><span data-stu-id="08e7f-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="08e7f-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="08e7f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="08e7f-106">使用者列表示例 Web 應用程式演示了使用 Razor 檢視引擎創建 ASP.NET MVC 3 應用程式是多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="08e7f-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="08e7f-107">該示例應用程式演示如何使用帶有 ASP.NET mVC 版本 3 和 Visual Studio 2010 的新 Razor 檢視引擎來創建虛構的使用者清單網站,該網站包含創建、顯示、編輯和刪除使用者等功能。</span><span class="sxs-lookup"><span data-stu-id="08e7f-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="08e7f-108">本教程介紹為生成使用者列表示例而採取的步驟ASP.NET MVC 3 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08e7f-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="08e7f-109">以 C# 與 VB 原始碼的視覺化工作室項目可隨同本主題:[下載](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。</span><span class="sxs-lookup"><span data-stu-id="08e7f-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="08e7f-110">如果您對本教程有疑問,請將其發佈到[MVC 論壇](https://forums.asp.net/1146.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08e7f-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="08e7f-111">總覽</span><span class="sxs-lookup"><span data-stu-id="08e7f-111">Overview</span></span>

<span data-ttu-id="08e7f-112">您將建置的應用程式是一個簡單的使用者清單網站。</span><span class="sxs-lookup"><span data-stu-id="08e7f-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="08e7f-113">用戶可以輸入、查看和更新使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="08e7f-113">Users can enter, view, and update user information.</span></span>

![範例網站](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="08e7f-115">您可以[在此處](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)下載 VB 和 C# 已完成的專案。</span><span class="sxs-lookup"><span data-stu-id="08e7f-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="08e7f-116">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="08e7f-116">Creating the Web Application</span></span>

<span data-ttu-id="08e7f-117">要開始本教程,請打開 Visual Studio 2010 並使用ASP.NET *MVC 3 Web 應用程式*樣本創建新專案。</span><span class="sxs-lookup"><span data-stu-id="08e7f-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="08e7f-118">命名應用程式&quot;Mvc3Razor&quot;。</span><span class="sxs-lookup"><span data-stu-id="08e7f-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="08e7f-119">[![新的 MVC 3 專案](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="08e7f-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="08e7f-120">在新**ASP.NET MVC 3 專案**對話方塊中,選擇 Internet**應用程式**,選擇 Razor 檢視引擎,然後單擊「**確定**」。</span><span class="sxs-lookup"><span data-stu-id="08e7f-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![新ASP.NET MVC 3 專案對話框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="08e7f-122">在本教學中,您將不使用ASP.NET成員資格提供者,因此您可以刪除與登錄和成員資格關聯的所有檔。</span><span class="sxs-lookup"><span data-stu-id="08e7f-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="08e7f-123">在**解決方案資源管理員中**,刪除以下檔案與目錄:</span><span class="sxs-lookup"><span data-stu-id="08e7f-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="08e7f-124">*控制器\帳戶控制器*</span><span class="sxs-lookup"><span data-stu-id="08e7f-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="08e7f-125">*模型_帳戶模型*</span><span class="sxs-lookup"><span data-stu-id="08e7f-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="08e7f-126">*檢視\共用\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="08e7f-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="08e7f-127">*檢視\帳號*(以及此目錄中的所有檔案)</span><span class="sxs-lookup"><span data-stu-id="08e7f-127">*Views\Account* (and all the files in this directory)</span></span>

![索倫·Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="08e7f-129">編輯<em>\_Layout.cshtml</em>檔,`<div>``logindisplay`並將命名 的元素內的標記<em>&quot;</em>替換為消息 「登錄&quot;禁用」。。</span><span class="sxs-lookup"><span data-stu-id="08e7f-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="08e7f-130">下面的範例顯示了新的標記:</span><span class="sxs-lookup"><span data-stu-id="08e7f-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="08e7f-131">新增模型</span><span class="sxs-lookup"><span data-stu-id="08e7f-131">Adding the Model</span></span>

<span data-ttu-id="08e7f-132">在 **「解決方案資源管理員」** 中,右鍵按*下模型模型資料夾*,選擇 **「添加**」,然後按下 **「類**」。</span><span class="sxs-lookup"><span data-stu-id="08e7f-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新使用者 Mdl 類別](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="08e7f-134">將類別命名為 `UserModel`。</span><span class="sxs-lookup"><span data-stu-id="08e7f-134">Name the class `UserModel`.</span></span> <span data-ttu-id="08e7f-135">將*UserModel*檔案的內容取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="08e7f-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="08e7f-136">類`UserModel`表示使用者。</span><span class="sxs-lookup"><span data-stu-id="08e7f-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="08e7f-137">類別每個成員都使用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的[「必需」](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性進行註解。</span><span class="sxs-lookup"><span data-stu-id="08e7f-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="08e7f-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空間中的屬性為 Web 應用程式提供自動用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="08e7f-139">開啟類別`HomeController`並新增`using`指令 ,以便您可以`UserModel``Users`存取 與類別:</span><span class="sxs-lookup"><span data-stu-id="08e7f-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="08e7f-140">聲明之後`HomeController`,添加以下註釋和`Users`對 類的引用:</span><span class="sxs-lookup"><span data-stu-id="08e7f-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="08e7f-141">該`Users`類是一個簡化的記憶體數據存儲,您將在本教程中使用。</span><span class="sxs-lookup"><span data-stu-id="08e7f-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="08e7f-142">在實際應用程式中,您將使用資料庫來存儲使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="08e7f-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="08e7f-143">`HomeController`該檔案的前幾行顯示在以下範例中:</span><span class="sxs-lookup"><span data-stu-id="08e7f-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="08e7f-144">生成應用程式,以便使用者模型在下一步中可供基架嚮導使用。</span><span class="sxs-lookup"><span data-stu-id="08e7f-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="08e7f-145">建立預設檢視</span><span class="sxs-lookup"><span data-stu-id="08e7f-145">Creating the Default View</span></span>

<span data-ttu-id="08e7f-146">下一步是添加一個操作方法和視圖來顯示使用者。</span><span class="sxs-lookup"><span data-stu-id="08e7f-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="08e7f-147">刪除現有的*檢視\Home_索引*檔。</span><span class="sxs-lookup"><span data-stu-id="08e7f-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="08e7f-148">您將創建新*的 Index*檔以顯示使用者。</span><span class="sxs-lookup"><span data-stu-id="08e7f-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="08e7f-149">在`HomeController`類別中,`Index`將方法的內容取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="08e7f-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="08e7f-150">右鍵按一下方法`Index`內 ,然後按下「**添加檢視**」。</span><span class="sxs-lookup"><span data-stu-id="08e7f-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![新增檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="08e7f-152">選擇「**創建強類型檢視**」 選項。</span><span class="sxs-lookup"><span data-stu-id="08e7f-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="08e7f-153">對於**查看資料類別**,請選擇**Mvc3Razor.Model.UserModel**。</span><span class="sxs-lookup"><span data-stu-id="08e7f-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="08e7f-154">(如果您沒有看到**Mvc3Razor.Models.UserModel**在 **"查看數據"類**框中,則需要生成專案。確保檢視引擎設定為**Razor**。</span><span class="sxs-lookup"><span data-stu-id="08e7f-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="08e7f-155">將 **「查看內容**」設置為 **「清單**」,然後按下「**添加**」 。</span><span class="sxs-lookup"><span data-stu-id="08e7f-155">Set **View content** to **List** and then click **Add**.</span></span>

![新增索引檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="08e7f-157">新檢視會自動對傳遞給`Index`檢視的用戶數據基腳架。</span><span class="sxs-lookup"><span data-stu-id="08e7f-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="08e7f-158">檢查新生成的*檢視\Home_Index*檔。</span><span class="sxs-lookup"><span data-stu-id="08e7f-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="08e7f-159">**"創建新**"、"**編輯**"、"**詳細資訊**"和 **"刪除**"連結不起作用,但頁面的其餘部分正常工作。</span><span class="sxs-lookup"><span data-stu-id="08e7f-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="08e7f-160">運行頁面。</span><span class="sxs-lookup"><span data-stu-id="08e7f-160">Run the page.</span></span> <span data-ttu-id="08e7f-161">您將看到使用者清單。</span><span class="sxs-lookup"><span data-stu-id="08e7f-161">You see a list of users.</span></span>

![索引頁](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="08e7f-163">開啟*Index.cshtml*檔案`ActionLink`,以以以下代碼取代**編輯**,**請詳細資訊**與**刪除**的標籤:</span><span class="sxs-lookup"><span data-stu-id="08e7f-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="08e7f-164">使用者名用作 ID,用於在 **「編輯**」、「**詳細資訊\*\*\*\*」和「刪除**」連結中尋找所選記錄。</span><span class="sxs-lookup"><span data-stu-id="08e7f-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="08e7f-165">建立詳細資訊檢視</span><span class="sxs-lookup"><span data-stu-id="08e7f-165">Creating the Details View</span></span>

<span data-ttu-id="08e7f-166">下一步是添加操作`Details`方法和視圖,以便顯示使用者詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="08e7f-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="08e7f-168">將以下`Details`方法加入主控制器:</span><span class="sxs-lookup"><span data-stu-id="08e7f-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="08e7f-169">右鍵按一下方法`Details`內 ,然後選擇<strong>「添加檢視</strong>」。。</span><span class="sxs-lookup"><span data-stu-id="08e7f-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="08e7f-170">認證<strong>「檢視資料類別」</strong>框是否包含<strong>Mvc3Razor.Model.UserModel</strong><em>。</em></span><span class="sxs-lookup"><span data-stu-id="08e7f-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="08e7f-171">將<strong>「查看內容」</strong>設定為<strong>「詳細資訊</strong>」,然後按下「<strong>添加</strong>」。</span><span class="sxs-lookup"><span data-stu-id="08e7f-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![新增詳細資訊檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="08e7f-173">運行應用程式並選擇詳細資訊連結。</span><span class="sxs-lookup"><span data-stu-id="08e7f-173">Run the application and select a details link.</span></span> <span data-ttu-id="08e7f-174">自動基架顯示模型中的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-174">The automatic scaffolding shows each property in the model.</span></span>

![詳細資料](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="08e7f-176">建立編輯檢視</span><span class="sxs-lookup"><span data-stu-id="08e7f-176">Creating the Edit View</span></span>

<span data-ttu-id="08e7f-177">將以下`Edit`方法添加到主控制器。</span><span class="sxs-lookup"><span data-stu-id="08e7f-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="08e7f-178">添加檢視與前面的步驟一樣,但將 **「查看內容」** 設定為 **「編輯**」。。</span><span class="sxs-lookup"><span data-stu-id="08e7f-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![新增編輯檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="08e7f-180">運行應用程式並編輯其中一個使用者的名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="08e7f-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="08e7f-181">如果違反了已應用於`DataAnnotation``UserModel`類的任何約束,則在提交表單時,將看到伺服器代碼生成的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="08e7f-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="08e7f-182">例如,如果在提交表單時將名字&quot;Ann&quot; &quot;&quot;更改為 A,則表單上將顯示以下錯誤:</span><span class="sxs-lookup"><span data-stu-id="08e7f-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="08e7f-183">在本教程中,您將使用者名視為主鍵。</span><span class="sxs-lookup"><span data-stu-id="08e7f-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="08e7f-184">因此,無法更改使用者名屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="08e7f-185">在*Edit.cshtml*檔中`Html.BeginForm`,在語句之後,將使用者名設置為隱藏欄位。</span><span class="sxs-lookup"><span data-stu-id="08e7f-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="08e7f-186">這將導致在模型中傳遞該屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="08e7f-187">以下片段顯示敘述的位置`Hidden`:</span><span class="sxs-lookup"><span data-stu-id="08e7f-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="08e7f-188">將`TextBoxFor`使用者名的`ValidationMessageFor`和標記替換為`DisplayFor`調用。</span><span class="sxs-lookup"><span data-stu-id="08e7f-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="08e7f-189">該方法`DisplayFor`將該屬性顯示為唯讀元素。</span><span class="sxs-lookup"><span data-stu-id="08e7f-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="08e7f-190">下列範例顯示完整的標記。</span><span class="sxs-lookup"><span data-stu-id="08e7f-190">The following example shows the completed markup.</span></span> <span data-ttu-id="08e7f-191">原始`TextBoxFor``ValidationMessageFor`與呼叫 Razor 開頭註解與結束註解字元`@* *@`() 註解出來</span><span class="sxs-lookup"><span data-stu-id="08e7f-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="08e7f-192">開啟客戶端驗證</span><span class="sxs-lookup"><span data-stu-id="08e7f-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="08e7f-193">要在 ASP.NET MVC 3 中啟用客戶端驗證,必須設置兩個標誌,並且必須包含三個 JavaScript 檔。</span><span class="sxs-lookup"><span data-stu-id="08e7f-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="08e7f-194">開啟應用程式的*Web.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="08e7f-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="08e7f-195">在`that ClientValidationEnabled`應用程式`UnobtrusiveJavaScriptEnabled`設定中驗證並設置為 true。</span><span class="sxs-lookup"><span data-stu-id="08e7f-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="08e7f-196">root *Web.config*檔案中的以下片段顯示了正確的設定:</span><span class="sxs-lookup"><span data-stu-id="08e7f-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="08e7f-197">設置為`UnobtrusiveJavaScriptEnabled`true 可實現不顯眼的 Ajax 和不顯眼的客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="08e7f-198">使用不顯眼的驗證時,驗證規則將轉換為 HTML5 屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="08e7f-199">HTML5 屬性名稱只能包含小寫字母、數位和破折號。</span><span class="sxs-lookup"><span data-stu-id="08e7f-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="08e7f-200">設置為`ClientValidationEnabled`true 啟用客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="08e7f-201">通過在應用程式*Web.config 檔中*設定這些金鑰,您可以為整個應用程式啟用客戶端驗證和不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="08e7f-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="08e7f-202">您可以使用以下代碼在單個檢視或控制器方法中啟用或關閉這些設定:</span><span class="sxs-lookup"><span data-stu-id="08e7f-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="08e7f-203">您還需要在呈現的檢視中包含多個 JavaScript 檔。</span><span class="sxs-lookup"><span data-stu-id="08e7f-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="08e7f-204">在所有檢視中包含 JavaScript 的一種簡單方法是將它們添加到*檢視_\\共用 _Layout.cshtml*檔中。</span><span class="sxs-lookup"><span data-stu-id="08e7f-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="08e7f-205">`<head>`*將\_Layout.cshtml*檔案的元素取代為以下代碼:</span><span class="sxs-lookup"><span data-stu-id="08e7f-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="08e7f-206">前兩個 jQuery 腳本由 Microsoft Ajax 內容交付網路 (CDN) 託管。</span><span class="sxs-lookup"><span data-stu-id="08e7f-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="08e7f-207">通過利用 Microsoft Ajax CDN,您可以顯著提高應用程式的第一熱性能。</span><span class="sxs-lookup"><span data-stu-id="08e7f-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="08e7f-208">運行應用程式並按一下編輯連結。</span><span class="sxs-lookup"><span data-stu-id="08e7f-208">Run the application and click an edit link.</span></span> <span data-ttu-id="08e7f-209">在瀏覽器中查看頁面的源。</span><span class="sxs-lookup"><span data-stu-id="08e7f-209">View the page's source in the browser.</span></span> <span data-ttu-id="08e7f-210">瀏覽器源顯示表單`data-val`的許多屬性(用於資料驗證)。</span><span class="sxs-lookup"><span data-stu-id="08e7f-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="08e7f-211">啟用客戶端驗證和不顯眼的 JavaScript 時,具有用戶端驗證規則的輸入欄`data-val="true"`位包含該 屬性以觸發不顯眼的客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="08e7f-212">例如,模型中的`City`欄位用[「必需」](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)屬性進行修飾,這將導致以下範例中顯示的 HTML:</span><span class="sxs-lookup"><span data-stu-id="08e7f-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="08e7f-213">對於每個用戶端驗證規則,將添加具有窗體`data-val-rulename="message"`的屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="08e7f-214">使用前面`City`顯示的欄位範例,所需的用戶端驗證規則將`data-val-required`生成 該屬性,&quot;並且消息「城市」欄位是必需&quot;的。</span><span class="sxs-lookup"><span data-stu-id="08e7f-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="08e7f-215">運行應用程式,編輯其中一個使用者,並清除該`City`欄位。</span><span class="sxs-lookup"><span data-stu-id="08e7f-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="08e7f-216">當您選項卡出欄位時,您將看到客戶端驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="08e7f-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![城市需要](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="08e7f-218">同樣,對於用戶端驗證規則中的每個參數,將添加具有窗體`data-val-rulename-paramname=paramvalue`的屬性。</span><span class="sxs-lookup"><span data-stu-id="08e7f-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="08e7f-219">例如,`FirstName`使用[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)屬性對屬性進行批號,並指定最小長度為 3 和最大長度為 8。</span><span class="sxs-lookup"><span data-stu-id="08e7f-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="08e7f-220">命名的`length`資料驗證規則具有參數`max`名稱 和參數值 8。</span><span class="sxs-lookup"><span data-stu-id="08e7f-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="08e7f-221">下面顯示了在編輯其中一個使用者時為`FirstName`字段產生的 HTML:</span><span class="sxs-lookup"><span data-stu-id="08e7f-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="08e7f-222">有關不顯眼的客戶端驗證的詳細資訊,請參閱 brad Wilson 博客[中ASP.NET MVC 3 中的"不顯眼客戶端驗證](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)"條目。</span><span class="sxs-lookup"><span data-stu-id="08e7f-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="08e7f-223">在ASP.NET MVC 3 測試版中,有時需要提交表單才能啟動客戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="08e7f-224">對於最終版本,可能會更改此情況。</span><span class="sxs-lookup"><span data-stu-id="08e7f-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="08e7f-225">建立檢視</span><span class="sxs-lookup"><span data-stu-id="08e7f-225">Creating the Create View</span></span>

<span data-ttu-id="08e7f-226">下一步是添加操作`Create`方法和視圖,以便使用戶能夠創建新使用者。</span><span class="sxs-lookup"><span data-stu-id="08e7f-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="08e7f-227">將以下`Create`方法加入主控制器:</span><span class="sxs-lookup"><span data-stu-id="08e7f-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="08e7f-228">添加檢視與前面的步驟一樣,但將 **「檢視內容」** 設定為 **「創建**」。。</span><span class="sxs-lookup"><span data-stu-id="08e7f-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![建立檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="08e7f-230">運行應用程式,選擇 **「創建**」連結,然後添加新使用者。</span><span class="sxs-lookup"><span data-stu-id="08e7f-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="08e7f-231">該方法`Create`會自動利用用戶端和伺服器端驗證。</span><span class="sxs-lookup"><span data-stu-id="08e7f-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="08e7f-232">嘗試輸入包含空白的使用者名稱,如&quot;Ben&quot;X 。</span><span class="sxs-lookup"><span data-stu-id="08e7f-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="08e7f-233">當您從使用者名稱選項卡外時,將顯示客戶端驗證錯誤 (`White space is not allowed`) 。</span><span class="sxs-lookup"><span data-stu-id="08e7f-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="08e7f-234">新增移除方法</span><span class="sxs-lookup"><span data-stu-id="08e7f-234">Add the Delete method</span></span>

<span data-ttu-id="08e7f-235">要完成本教學,請向主控制器`Delete`添加以下方法:</span><span class="sxs-lookup"><span data-stu-id="08e7f-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="08e7f-236">新增`Delete`檢視,如前面的步驟,**將"查看內容"** 設定為 **"刪除**"。</span><span class="sxs-lookup"><span data-stu-id="08e7f-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![刪除檢視](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="08e7f-238">現在,您擁有一個簡單但功能齊全ASP.NET MVC 3 應用程式,並具有驗證功能。</span><span class="sxs-lookup"><span data-stu-id="08e7f-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
