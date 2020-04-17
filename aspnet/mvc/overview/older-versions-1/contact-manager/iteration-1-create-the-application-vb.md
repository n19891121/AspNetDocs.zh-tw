---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
title: 反覆運算#1 = 建立應用程式 (VB) |微軟文件
author: rick-anderson
description: 在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。 我們增加了對基本資料庫操作的支援:創建、讀取、更新和 D...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 5b033582-1646-42c2-b20d-7edc8814e970
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-vb
msc.type: authoredcontent
ms.openlocfilehash: 235f6f8812a2f584de8e07dcf97d5c1712c51776
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542530"
---
# <a name="iteration-1--create-the-application-vb"></a><span data-ttu-id="616d8-104">反覆項目 #1 – 建立應用程式 (VB)</span><span class="sxs-lookup"><span data-stu-id="616d8-104">Iteration #1 – Create the Application (VB)</span></span>

<span data-ttu-id="616d8-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="616d8-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="616d8-106">下載代碼</span><span class="sxs-lookup"><span data-stu-id="616d8-106">Download Code</span></span>](iteration-1-create-the-application-vb/_static/contactmanager_1_vb1.zip)

> <span data-ttu-id="616d8-107">在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。</span><span class="sxs-lookup"><span data-stu-id="616d8-107">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="616d8-108">我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="616d8-108">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="616d8-109">建構 MVC 應用程式 (VB) ASP.NET連絡人管理</span><span class="sxs-lookup"><span data-stu-id="616d8-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="616d8-110">在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="616d8-111">透過聯絡人管理員應用程式,您可以儲存連絡人資訊 (姓名、電話號碼和電子郵件位址) 人員清單。</span><span class="sxs-lookup"><span data-stu-id="616d8-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="616d8-112">我們通過多次反覆運算構建應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="616d8-113">每次反覆運算時,我們都會逐步改進應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="616d8-114">此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。</span><span class="sxs-lookup"><span data-stu-id="616d8-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="616d8-115">反覆運算#1 - 創建應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="616d8-116">在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。</span><span class="sxs-lookup"><span data-stu-id="616d8-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="616d8-117">我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="616d8-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="616d8-118">反覆運算#2 - 使應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="616d8-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="616d8-119">在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="616d8-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="616d8-120">反覆運算#3 - 添加表單驗證。</span><span class="sxs-lookup"><span data-stu-id="616d8-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="616d8-121">在第三個反覆運算中,我們添加基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="616d8-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="616d8-122">我們防止人們在未填寫所需表單欄位的情況下提交表單。</span><span class="sxs-lookup"><span data-stu-id="616d8-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="616d8-123">我們還驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="616d8-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="616d8-124">反覆運算#4 - 使應用程式鬆散耦合。</span><span class="sxs-lookup"><span data-stu-id="616d8-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="616d8-125">在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="616d8-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="616d8-126">例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。</span><span class="sxs-lookup"><span data-stu-id="616d8-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="616d8-127">反覆運算#5 - 創建單元測試。</span><span class="sxs-lookup"><span data-stu-id="616d8-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="616d8-128">在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。</span><span class="sxs-lookup"><span data-stu-id="616d8-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="616d8-129">我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。</span><span class="sxs-lookup"><span data-stu-id="616d8-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="616d8-130">反覆運算#6 - 使用測試驅動開發。</span><span class="sxs-lookup"><span data-stu-id="616d8-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="616d8-131">在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。</span><span class="sxs-lookup"><span data-stu-id="616d8-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="616d8-132">在此反覆運算中,我們添加聯繫人組。</span><span class="sxs-lookup"><span data-stu-id="616d8-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="616d8-133">反覆運算#7 - 添加Ajax功能。</span><span class="sxs-lookup"><span data-stu-id="616d8-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="616d8-134">在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。</span><span class="sxs-lookup"><span data-stu-id="616d8-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="616d8-135">此反覆運算</span><span class="sxs-lookup"><span data-stu-id="616d8-135">This Iteration</span></span>

<span data-ttu-id="616d8-136">在第一次反覆運算中,我們將構建基本應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-136">In this first iteration, we build the basic application.</span></span> <span data-ttu-id="616d8-137">目標是以最快、最簡單的方式構建聯繫人管理器。</span><span class="sxs-lookup"><span data-stu-id="616d8-137">The goal is to build the Contact Manager in the fastest and simplest way possible.</span></span> <span data-ttu-id="616d8-138">在以後的反覆運算中,我們改進了應用程式的設計。</span><span class="sxs-lookup"><span data-stu-id="616d8-138">In later iterations, we improve the design of the application.</span></span>

<span data-ttu-id="616d8-139">聯繫人管理器應用程式是一個基本的資料庫驅動應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-139">The Contact Manager application is a basic database-driven application.</span></span> <span data-ttu-id="616d8-140">您可以使用該應用程式創建新連絡人、編輯現有連絡人和刪除連絡人。</span><span class="sxs-lookup"><span data-stu-id="616d8-140">You can use the application to create new contacts, edit existing contacts, and delete contacts.</span></span>

<span data-ttu-id="616d8-141">在此反覆運算中,我們完成以下步驟:</span><span class="sxs-lookup"><span data-stu-id="616d8-141">In this iteration, we complete the following steps:</span></span>

1. <span data-ttu-id="616d8-142">ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="616d8-142">ASP.NET MVC application</span></span>
2. <span data-ttu-id="616d8-143">建立資料庫以儲存我們的聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-143">Create a database to store our contacts</span></span>
3. <span data-ttu-id="616d8-144">使用 Microsoft 實體架構為資料庫產生模型類別</span><span class="sxs-lookup"><span data-stu-id="616d8-144">Generate a model class for our database with the Microsoft Entity Framework</span></span>
4. <span data-ttu-id="616d8-145">建立控制器操作與檢視,讓我們能夠列出資料庫中的所有聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-145">Create a controller action and view that enables us to list all of the contacts in the database</span></span>
5. <span data-ttu-id="616d8-146">建立控制器操作與檢視,讓我們能夠建立新聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-146">Create controller actions and a view that enables us to create a new contact in the database</span></span>
6. <span data-ttu-id="616d8-147">建立控制器操作與檢視,讓我們可以編輯資料庫中的現有聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-147">Create controller actions and a view that enables us to edit an existing contact in the database</span></span>
7. <span data-ttu-id="616d8-148">建立控制器操作與檢視,讓我們能夠移除資料庫中的現有聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-148">Create controller actions and a view that enables us to delete an existing contact in the database</span></span>

## <a name="software-prerequisites"></a><span data-ttu-id="616d8-149">軟體必要條件</span><span class="sxs-lookup"><span data-stu-id="616d8-149">Software Prerequisites</span></span>

<span data-ttu-id="616d8-150">在ASP.NET MVC 應用程式中,必須在您的電腦上安裝 Visual Studio 2008 或 Visual Web 開發人員 2008(可視化 Web 開發人員是 Visual Studio 的免費版本,不包含 Visual Studio 的所有高級功能)。</span><span class="sxs-lookup"><span data-stu-id="616d8-150">In ASP.NET MVC applications, you must have either Visual Studio 2008 or Visual Web Developer 2008 installed on your computer (Visual Web Developer is a free version of Visual Studio that does not include all of the advanced features of Visual Studio).</span></span> <span data-ttu-id="616d8-151">您可以透過以下位址下載 Visual Studio 2008 試用版或視覺化 Web 開發人員版本:</span><span class="sxs-lookup"><span data-stu-id="616d8-151">You can download either the trial version of Visual Studio 2008 or Visual Web Developer from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> <span data-ttu-id="616d8-152">對於具有視覺化 Web 開發人員 ASP.NET MVC 應用程式,必須安裝可視化 Web 開發人員服務包 1。</span><span class="sxs-lookup"><span data-stu-id="616d8-152">For ASP.NET MVC applications with Visual Web Developer, you must have Visual Web Developer Service Pack 1 installed.</span></span> <span data-ttu-id="616d8-153">如果沒有服務包 1,則無法創建 Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="616d8-153">Without Service Pack 1, you cannot create Web Application Projects.</span></span>

<span data-ttu-id="616d8-154">ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="616d8-154">ASP.NET MVC framework.</span></span> <span data-ttu-id="616d8-155">可以從以下位址下載ASP.NET MVC 框架:</span><span class="sxs-lookup"><span data-stu-id="616d8-155">You can download the ASP.NET MVC framework from the following address:</span></span>

[https://www.asp.net/mvc](../../../index.md)

<span data-ttu-id="616d8-156">在本教學中,我們使用Microsoft實體框架訪問資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-156">In this tutorial, we use the Microsoft Entity Framework to access a database.</span></span> <span data-ttu-id="616d8-157">實體框架包含在 .NET 框架 3.5 服務包 1 中。</span><span class="sxs-lookup"><span data-stu-id="616d8-157">The Entity Framework is included with .NET Framework 3.5 Service Pack 1.</span></span> <span data-ttu-id="616d8-158">您可以透過以下位置下載此服務套件:</span><span class="sxs-lookup"><span data-stu-id="616d8-158">You can download this service pack from the following location:</span></span>

[<span data-ttu-id="616d8-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d斯普拉朗</span><span class="sxs-lookup"><span data-stu-id="616d8-159">https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

<span data-ttu-id="616d8-160">作為逐個執行每個下載的替代方法,您可以利用 Web 平臺安裝程式 (Web PI)。</span><span class="sxs-lookup"><span data-stu-id="616d8-160">As an alternative to performing each of these downloads one by one, you can take advantage of the Web Platform Installer (Web PI).</span></span> <span data-ttu-id="616d8-161">您可以透過以下位址下載 Web PI:</span><span class="sxs-lookup"><span data-stu-id="616d8-161">You can download the Web PI from the following address:</span></span>

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a><span data-ttu-id="616d8-162">ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="616d8-162">ASP.NET MVC Project</span></span>

<span data-ttu-id="616d8-163">ASP.NET MVC Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="616d8-163">ASP.NET MVC Web Application Project.</span></span> <span data-ttu-id="616d8-164">啟動視覺化工作室並選擇選單選項**檔案,新專案**。</span><span class="sxs-lookup"><span data-stu-id="616d8-164">Launch Visual Studio and select the menu option **File, New Project**.</span></span> <span data-ttu-id="616d8-165">將顯示 **「新專案」** 對話框(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="616d8-165">The **New Project** dialog appears (see Figure 1).</span></span> <span data-ttu-id="616d8-166">選擇**Web**專案類型和**ASP.NET MVC Web 應用程式**樣本。</span><span class="sxs-lookup"><span data-stu-id="616d8-166">Select the **Web** project type and the **ASP.NET MVC Web Application** template.</span></span> <span data-ttu-id="616d8-167">說出您的新項目*聯繫人管理器*,然後按下"確定"按鈕。</span><span class="sxs-lookup"><span data-stu-id="616d8-167">Name your new project *ContactManager* and click the OK button.</span></span>

<span data-ttu-id="616d8-168">請確保從 **「新專案」** 對話框右上角的下拉清單中選擇了 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="616d8-168">Make sure that you have .NET Framework 3.5 selected from the dropdown list at the top right of the **New Project** dialog.</span></span> <span data-ttu-id="616d8-169">否則,將不會顯示ASP.NET MVC Web 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="616d8-169">Otherwise, the ASP.NET MVC Web Application template won't appear.</span></span>

<span data-ttu-id="616d8-170">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-170">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image1.jpg)](iteration-1-create-the-application-vb/_static/image1.png)</span></span>

<span data-ttu-id="616d8-171">**圖 01**: 新的項目對話框([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-171">**Figure 01**: The New Project dialog([Click to view full-size image](iteration-1-create-the-application-vb/_static/image2.png))</span></span>

<span data-ttu-id="616d8-172">ASP.NET MVC 應用程式,將顯示 **「創建單元測試項目**」對話方塊。</span><span class="sxs-lookup"><span data-stu-id="616d8-172">ASP.NET MVC application, the **Create Unit Test Project** dialog appears.</span></span> <span data-ttu-id="616d8-173">可以使用此對話方塊指示在創建ASP.NET MVC 應用程式時要創建單元測試專案並將其添加到解決方案中。</span><span class="sxs-lookup"><span data-stu-id="616d8-173">You can use this dialog to indicate that you want to create and add a unit test project to your solution when you create your ASP.NET MVC application.</span></span> <span data-ttu-id="616d8-174">儘管我們在此反覆運算中不會構建單元測試,但應選擇選項 **「是」,創建單元測試專案**,因為我們計劃在以後的反覆運算中添加單元測試。</span><span class="sxs-lookup"><span data-stu-id="616d8-174">Although we won't be building unit tests in this iteration, you should select the option **Yes, create a unit test project** because we plan to add unit tests in a later iteration.</span></span> <span data-ttu-id="616d8-175">首次創建新的ASP.NET MVC 專案時添加測試專案比創建ASP.NET MVC 專案後添加測試專案要容易得多。</span><span class="sxs-lookup"><span data-stu-id="616d8-175">Adding a Test project when you first create a new ASP.NET MVC project is much easier than adding a Test project after the ASP.NET MVC project has been created.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="616d8-176">由於視覺化 Web 開發人員不支援測試專案,因此在使用可視化 Web 開發人員時,您不會獲取「創建單元測試專案」 對話框。</span><span class="sxs-lookup"><span data-stu-id="616d8-176">Because Visual Web Developer does not support Test projects, you do not get the Create Unit Test Project dialog when using Visual Web Developer.</span></span>

<span data-ttu-id="616d8-177">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-177">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image2.jpg)](iteration-1-create-the-application-vb/_static/image3.png)</span></span>

<span data-ttu-id="616d8-178">**圖 02**: 建立單元測試項目對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-178">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image4.png))</span></span>

<span data-ttu-id="616d8-179">ASP.NET MVC 應用程式顯示在可視化工作室解決方案資源管理器視窗中(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="616d8-179">ASP.NET MVC application appears in the Visual Studio Solution Explorer window (see Figure 3).</span></span> <span data-ttu-id="616d8-180">如果看不到"解決方案資源管理器"視窗,則可以通過選擇功能表選項 **"視圖"、"解決方案資源管理員**"來打開此視窗。</span><span class="sxs-lookup"><span data-stu-id="616d8-180">If you don t see the Solution Explorer window then you can open this window by selecting the menu option **View, Solution Explorer**.</span></span> <span data-ttu-id="616d8-181">請注意,該解決方案包含兩個專案:ASP.NET MVC 專案和測試專案。</span><span class="sxs-lookup"><span data-stu-id="616d8-181">Notice that the solution contains two projects: the ASP.NET MVC project and the Test project.</span></span> <span data-ttu-id="616d8-182">mVCASP.NET專案命名為"連絡人管理器",測試專案命名為"連絡人管理器"。</span><span class="sxs-lookup"><span data-stu-id="616d8-182">The ASP.NET MVC project is named ContactManager and the Test project is named ContactManager.Tests.</span></span>

<span data-ttu-id="616d8-183">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-183">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image3.jpg)](iteration-1-create-the-application-vb/_static/image5.png)</span></span>

<span data-ttu-id="616d8-184">**圖 03**: 解決方案資源管理員視窗 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-184">**Figure 03**: The Solution Explorer window ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image6.png))</span></span>

## <a name="deleting-the-project-sample-files"></a><span data-ttu-id="616d8-185">刪除項目範例檔案</span><span class="sxs-lookup"><span data-stu-id="616d8-185">Deleting the Project Sample Files</span></span>

<span data-ttu-id="616d8-186">ASP.NET MVC 專案範本包括控制器和檢視的範例檔。</span><span class="sxs-lookup"><span data-stu-id="616d8-186">The ASP.NET MVC project template includes sample files for controllers and views.</span></span> <span data-ttu-id="616d8-187">在創建新ASP.NET MVC 應用程式之前,應刪除這些檔。</span><span class="sxs-lookup"><span data-stu-id="616d8-187">Before creating a new ASP.NET MVC application, you should delete these files.</span></span> <span data-ttu-id="616d8-188">您可以通過右鍵單擊檔或資料夾並選擇功能表選項 **「刪除**」來刪除解決方案資源管理器視窗中的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="616d8-188">You can delete files and folders in the Solution Explorer window by right-clicking a file or folder and selecting the menu option **Delete**.</span></span>

<span data-ttu-id="616d8-189">您需要從 ASP.NET MVC 項目中移除以下檔案:</span><span class="sxs-lookup"><span data-stu-id="616d8-189">You need to delete the following files from the ASP.NET MVC project:</span></span>

- <span data-ttu-id="616d8-190">[控制器]主控制器.vb</span><span class="sxs-lookup"><span data-stu-id="616d8-190">\Controllers\HomeController.vb</span></span>

- <span data-ttu-id="616d8-191">[視圖]主頁\關於.aspx</span><span class="sxs-lookup"><span data-stu-id="616d8-191">\Views\Home\About.aspx</span></span>

- <span data-ttu-id="616d8-192">[視圖]主頁\索引.aspx</span><span class="sxs-lookup"><span data-stu-id="616d8-192">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="616d8-193">而且,您需要從測試項目中刪除以下檔:</span><span class="sxs-lookup"><span data-stu-id="616d8-193">And, you need to delete the following file from the Test project:</span></span>

<span data-ttu-id="616d8-194">[控制器]主控制器測試.vb</span><span class="sxs-lookup"><span data-stu-id="616d8-194">\Controllers\HomeControllerTest.vb</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="616d8-195">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="616d8-195">Creating the Database</span></span>

<span data-ttu-id="616d8-196">連絡人管理員應用程式是資料庫驅動的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-196">The Contact Manager application is a database-driven web application.</span></span> <span data-ttu-id="616d8-197">我們使用資料庫來存儲聯繫資訊。</span><span class="sxs-lookup"><span data-stu-id="616d8-197">We use a database to store the contact information.</span></span>

<span data-ttu-id="616d8-198">ASP.NET MVC 框架,包含任何現代資料庫,包括 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-198">The ASP.NET MVC framework with any modern database including Microsoft SQL Server, Oracle, MySQL, and IBM DB2 databases.</span></span> <span data-ttu-id="616d8-199">在本教學中,我們使用Microsoft SQL Server資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-199">In this tutorial, we use a Microsoft SQL Server database.</span></span> <span data-ttu-id="616d8-200">安裝 Visual Studio 時,系統會提供安裝 Microsoft SQL Server Express 的選項,這是 Microsoft SQL Server 資料庫的免費版本。</span><span class="sxs-lookup"><span data-stu-id="616d8-200">When you install Visual Studio, you are provided with the option of installing Microsoft SQL Server Express which is a free version of the Microsoft SQL Server database.</span></span>

<span data-ttu-id="616d8-201">通過右鍵單擊解決方案資源管理器視窗中的應用\_資料資料夾並選擇功能表選項 **「添加、新專案**」來創建新資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-201">Create a new database by right-clicking the App\_Data folder in the Solution Explorer window and selecting the menu option **Add, New Item**.</span></span> <span data-ttu-id="616d8-202">在 **「新增新項目」** 對話方塊中,選擇 **「資料**」類別和**SQL Server 資料庫**樣本(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="616d8-202">In the **Add New Item** dialog, select the **Data** category and the **SQL Server Database** template (see Figure 4).</span></span> <span data-ttu-id="616d8-203">命名新資料庫 ContactManagerDB.mdf,然後單擊"確定"按鈕。</span><span class="sxs-lookup"><span data-stu-id="616d8-203">Name the new database ContactManagerDB.mdf and click the OK button.</span></span>

<span data-ttu-id="616d8-204">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-204">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image4.jpg)](iteration-1-create-the-application-vb/_static/image7.png)</span></span>

<span data-ttu-id="616d8-205">**圖04**:建立新的微軟 SQL Server Express 資料庫 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-205">**Figure 04**: Creating a new Microsoft SQL Server Express database ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image8.png))</span></span>

<span data-ttu-id="616d8-206">創建新資料庫後,資料庫將顯示在解決方案資源管理器視窗中的應用\_資料資料夾中。</span><span class="sxs-lookup"><span data-stu-id="616d8-206">After you create the new database, the database appears in the App\_Data folder in the Solution Explorer window.</span></span> <span data-ttu-id="616d8-207">按兩下 ContactManager.mdf 檔案以開啟伺服器資源管理員視窗並連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-207">Double-click the ContactManager.mdf file to open the Server Explorer window and connect to the database.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="616d8-208">伺服器資源管理員窗口稱為資料庫資源管理員視窗(對於Microsoft視覺化Web開發人員)。</span><span class="sxs-lookup"><span data-stu-id="616d8-208">The Server Explorer window is called the Database Explorer window in the case of Microsoft Visual Web Developer.</span></span>

<span data-ttu-id="616d8-209">可以使用 Server 資源管理器視窗創建新的資料庫物件,如資料庫表、視圖、觸發器和儲存過程。</span><span class="sxs-lookup"><span data-stu-id="616d8-209">You can use the Server Explorer window to create new database objects such as database tables, views, triggers, and stored procedures.</span></span> <span data-ttu-id="616d8-210">右鍵按下「表」資料夾並選擇功能表選項 **「新增新表**」。。</span><span class="sxs-lookup"><span data-stu-id="616d8-210">Right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="616d8-211">將顯示資料庫表設計器(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="616d8-211">The Database Table Designer appears (see Figure 5).</span></span>

<span data-ttu-id="616d8-212">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-212">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image5.jpg)](iteration-1-create-the-application-vb/_static/image9.png)</span></span>

<span data-ttu-id="616d8-213">**圖 05**: 資料庫表設計器 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-213">**Figure 05**: The Database Table Designer ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image10.png))</span></span>

<span data-ttu-id="616d8-214">我們需要建立以下欄的表格:</span><span class="sxs-lookup"><span data-stu-id="616d8-214">We need to create a table that contains the following columns:</span></span>

<a id="0.2_table01"></a>

| <span data-ttu-id="616d8-215">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="616d8-215">**Column Name**</span></span> | <span data-ttu-id="616d8-216">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="616d8-216">**Data Type**</span></span> | <span data-ttu-id="616d8-217">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="616d8-217">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="616d8-218">Id</span><span class="sxs-lookup"><span data-stu-id="616d8-218">Id</span></span> | <span data-ttu-id="616d8-219">int</span><span class="sxs-lookup"><span data-stu-id="616d8-219">int</span></span> | <span data-ttu-id="616d8-220">false</span><span class="sxs-lookup"><span data-stu-id="616d8-220">false</span></span> |
| <span data-ttu-id="616d8-221">名字</span><span class="sxs-lookup"><span data-stu-id="616d8-221">FirstName</span></span> | <span data-ttu-id="616d8-222">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="616d8-222">nvarchar(50)</span></span> | <span data-ttu-id="616d8-223">false</span><span class="sxs-lookup"><span data-stu-id="616d8-223">false</span></span> |
| <span data-ttu-id="616d8-224">姓氏</span><span class="sxs-lookup"><span data-stu-id="616d8-224">LastName</span></span> | <span data-ttu-id="616d8-225">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="616d8-225">nvarchar(50)</span></span> | <span data-ttu-id="616d8-226">false</span><span class="sxs-lookup"><span data-stu-id="616d8-226">false</span></span> |
| <span data-ttu-id="616d8-227">電話</span><span class="sxs-lookup"><span data-stu-id="616d8-227">Phone</span></span> | <span data-ttu-id="616d8-228">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="616d8-228">nvarchar(50)</span></span> | <span data-ttu-id="616d8-229">false</span><span class="sxs-lookup"><span data-stu-id="616d8-229">false</span></span> |
| <span data-ttu-id="616d8-230">電子郵件</span><span class="sxs-lookup"><span data-stu-id="616d8-230">Email</span></span> | <span data-ttu-id="616d8-231">nvarchar(255)</span><span class="sxs-lookup"><span data-stu-id="616d8-231">nvarchar(255)</span></span> | <span data-ttu-id="616d8-232">false</span><span class="sxs-lookup"><span data-stu-id="616d8-232">false</span></span> |

<span data-ttu-id="616d8-233">第一列"Id"列是特殊的。</span><span class="sxs-lookup"><span data-stu-id="616d8-233">The first column, the Id column, is special.</span></span> <span data-ttu-id="616d8-234">您需要將 Id 列標記為識別列和主鍵列。</span><span class="sxs-lookup"><span data-stu-id="616d8-234">You need to mark the Id column as an Identity column and a Primary Key column.</span></span> <span data-ttu-id="616d8-235">通過展開列屬性(查看圖 6 的底部)向下滾動到標識規範屬性,指示列是標識列。</span><span class="sxs-lookup"><span data-stu-id="616d8-235">You indicate that a column is an Identity column by expanding Column Properties (look at the bottom of Figure 6) and scrolling down to the Identity Specification property.</span></span> <span data-ttu-id="616d8-236">將 **(是識別)** 屬性設定為值**是**。</span><span class="sxs-lookup"><span data-stu-id="616d8-236">Set the **(Is Identity)** property to the value **Yes**.</span></span>

<span data-ttu-id="616d8-237">通過選擇列並按一下帶有鍵圖示的按鈕,將列標記為主鍵列。</span><span class="sxs-lookup"><span data-stu-id="616d8-237">You mark a column as a Primary Key column by selecting the column and clicking the button with the icon of a key.</span></span> <span data-ttu-id="616d8-238">將列標記為主鍵列后,列旁邊將顯示一個鍵圖示(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="616d8-238">After a column is marked as a Primary Key column, an icon of a key appears next to the column (see Figure 6).</span></span>

<span data-ttu-id="616d8-239">完成表創建後,按下「儲存」按鈕(帶有軟盤圖示的按鈕)以保存新錶。</span><span class="sxs-lookup"><span data-stu-id="616d8-239">After you finish creating the table, click the Save button (the button with an icon of a floppy) to save the new table.</span></span> <span data-ttu-id="616d8-240">為您的新表命名 *「連絡人*」。</span><span class="sxs-lookup"><span data-stu-id="616d8-240">Give your new table the name *Contacts*.</span></span>

<span data-ttu-id="616d8-241">完成創建"連絡人"資料庫表後,應向該表添加一些記錄。</span><span class="sxs-lookup"><span data-stu-id="616d8-241">After finish creating the Contacts database table, you should add some records to the table.</span></span> <span data-ttu-id="616d8-242">右鍵按一下伺服器資源管理器視窗中的"連絡人"表,然後選擇功能表選項 **"顯示表資料**"。</span><span class="sxs-lookup"><span data-stu-id="616d8-242">Right-click the Contacts table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="616d8-243">在顯示的網格中輸入一個或多個聯繫人。</span><span class="sxs-lookup"><span data-stu-id="616d8-243">Enter one or more contacts in the grid that appears.</span></span>

## <a name="creating-the-data-model"></a><span data-ttu-id="616d8-244">建立資料模型</span><span class="sxs-lookup"><span data-stu-id="616d8-244">Creating the Data Model</span></span>

<span data-ttu-id="616d8-245">ASP.NET MVC 應用程式由模型、視圖和控制器組成。</span><span class="sxs-lookup"><span data-stu-id="616d8-245">The ASP.NET MVC application consists of Models, Views, and Controllers.</span></span> <span data-ttu-id="616d8-246">我們首先創建一個模型類,該類表示我們在上一節中創建的"連絡人"表。</span><span class="sxs-lookup"><span data-stu-id="616d8-246">We start by creating a Model class that represents the Contacts table that we created in the previous section.</span></span>

<span data-ttu-id="616d8-247">在本教學中,我們使用Microsoft實體框架從資料庫自動生成模型類。</span><span class="sxs-lookup"><span data-stu-id="616d8-247">In this tutorial, we use the Microsoft Entity Framework to generate a model class from the database automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="616d8-248">ASP.NET MVC 框架不以任何方式綁定到 Microsoft 實體框架。</span><span class="sxs-lookup"><span data-stu-id="616d8-248">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework in any way.</span></span> <span data-ttu-id="616d8-249">您可以將mVCASP.NET替代資料庫存取技術(包括 NHibernate、LINQ 到 SQL 或ADO.NET) 使用。</span><span class="sxs-lookup"><span data-stu-id="616d8-249">You can use ASP.NET MVC with alternative database access technologies including NHibernate, LINQ to SQL, or ADO.NET.</span></span>

<span data-ttu-id="616d8-250">依以下步驟建立資料模型類別:</span><span class="sxs-lookup"><span data-stu-id="616d8-250">Follow these steps to create the data model classes:</span></span>

1. <span data-ttu-id="616d8-251">右鍵按下「解決方案資源管理器」視窗中的「模型」資料夾,然後選擇「**添加新專案**」。</span><span class="sxs-lookup"><span data-stu-id="616d8-251">Right-click the Models folder in the Solution Explorer window and select **Add, New Item**.</span></span> <span data-ttu-id="616d8-252">將顯示 **「添加新專案」** 對話框(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="616d8-252">The **Add New Item** dialog appears (see Figure 6).</span></span>
2. <span data-ttu-id="616d8-253">選擇 **「資料**」類別和**ADO.NET 實體資料模型**樣本。</span><span class="sxs-lookup"><span data-stu-id="616d8-253">Select the **Data** category and the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="616d8-254">命名資料模型*ContactManagerModel.edmx,* 然後按下 **「添加**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="616d8-254">Name your data model *ContactManagerModel.edmx* and click the **Add** button.</span></span> <span data-ttu-id="616d8-255">將顯示實體數據模型向導(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="616d8-255">The Entity Data Model wizard appears (see Figure 7).</span></span>
3. <span data-ttu-id="616d8-256">在 **「選擇模型內容」** 步驟中,選擇**從資料庫中生成**(參見圖 7)。</span><span class="sxs-lookup"><span data-stu-id="616d8-256">In the **Choose Model Contents** step, select **Generate from database** (see Figure 7).</span></span>
4. <span data-ttu-id="616d8-257">在 **「選擇資料連線**」步驟中,選擇 ContactManagerDB.mdf 資料庫,並輸入實體連接設定的名稱 *「連絡人管理器資料庫實體*」(參見圖 8)。</span><span class="sxs-lookup"><span data-stu-id="616d8-257">In the **Choose Your Data Connection** step, select the ContactManagerDB.mdf database and enter the name *ContactManagerDBEntities* for the Entity Connection Settings (see Figure 8).</span></span>
5. <span data-ttu-id="616d8-258">在 **「選擇資料庫物件**」步驟中,選擇標記為表的複選框(參見圖 9)。</span><span class="sxs-lookup"><span data-stu-id="616d8-258">In the **Choose Your Database Objects** step, select the checkbox labeled Tables (see Figure 9).</span></span> <span data-ttu-id="616d8-259">數據模型將包括資料庫中包含的所有表(只有一個,"連絡人"表)。</span><span class="sxs-lookup"><span data-stu-id="616d8-259">The data model will include all tables contained in your database (there is just one, the Contacts table).</span></span> <span data-ttu-id="616d8-260">輸入命名空間*模型*。</span><span class="sxs-lookup"><span data-stu-id="616d8-260">Enter the namespace *Models*.</span></span> <span data-ttu-id="616d8-261">按下「完成」按鈕以完成嚮導。</span><span class="sxs-lookup"><span data-stu-id="616d8-261">Click the Finish button to complete the wizard.</span></span>

<span data-ttu-id="616d8-262">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-262">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image6.jpg)](iteration-1-create-the-application-vb/_static/image11.png)</span></span>

<span data-ttu-id="616d8-263">**圖 06**: 新增新項目對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-263">**Figure 06**: The Add New Item dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image12.png))</span></span>

<span data-ttu-id="616d8-264">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-264">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image7.jpg)](iteration-1-create-the-application-vb/_static/image13.png)</span></span>

<span data-ttu-id="616d8-265">**圖 07**: 選擇模型內容 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-265">**Figure 07**: Choose Model Contents ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image14.png))</span></span>

<span data-ttu-id="616d8-266">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-266">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image8.jpg)](iteration-1-create-the-application-vb/_static/image15.png)</span></span>

<span data-ttu-id="616d8-267">**圖 08**: 選擇您的資料連線 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-267">**Figure 08**: Choose Your Data Connection ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image16.png))</span></span>

<span data-ttu-id="616d8-268">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-268">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image9.jpg)](iteration-1-create-the-application-vb/_static/image17.png)</span></span>

<span data-ttu-id="616d8-269">**圖 09**: 選擇資料庫物件([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-269">**Figure 09**: Choose Your Database Objects ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image18.png))</span></span>

<span data-ttu-id="616d8-270">完成實體數據模型嚮導後,將顯示實體數據模型設計器。</span><span class="sxs-lookup"><span data-stu-id="616d8-270">After you complete the Entity Data Model Wizard, the Entity Data Model Designer appears.</span></span> <span data-ttu-id="616d8-271">設計器顯示與要建模的每個表對應的類。</span><span class="sxs-lookup"><span data-stu-id="616d8-271">The designer displays a class that corresponds to each table being modeled.</span></span> <span data-ttu-id="616d8-272">您應該會看到一個名為"連絡人"的類。</span><span class="sxs-lookup"><span data-stu-id="616d8-272">You should see one class named Contacts.</span></span>

<span data-ttu-id="616d8-273">實體數據模型向導基於資料庫表名稱生成類名稱。</span><span class="sxs-lookup"><span data-stu-id="616d8-273">The Entity Data Model wizard generates class names based on database table names.</span></span> <span data-ttu-id="616d8-274">您幾乎總是需要更改精靈產生的類的名稱。</span><span class="sxs-lookup"><span data-stu-id="616d8-274">You almost always need to change the name of the class generated by the wizard.</span></span> <span data-ttu-id="616d8-275">右鍵單擊設計器中的"連絡人"類,然後選擇功能表選項 **"重新命名**。</span><span class="sxs-lookup"><span data-stu-id="616d8-275">Right-click the Contacts class in the designer and select the menu option **Rename**.</span></span> <span data-ttu-id="616d8-276">將類的名稱從"連絡人"(複數)更改為"連絡人"(單數)。</span><span class="sxs-lookup"><span data-stu-id="616d8-276">Change the name of the class from Contacts (plural) to Contact (singular).</span></span> <span data-ttu-id="616d8-277">更改類名稱后,類應如下所示 10。</span><span class="sxs-lookup"><span data-stu-id="616d8-277">After you change the class name, the class should appear like Figure 10.</span></span>

<span data-ttu-id="616d8-278">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-278">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image10.jpg)](iteration-1-create-the-application-vb/_static/image19.png)</span></span>

<span data-ttu-id="616d8-279">**圖10**: 連絡人類 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-279">**Figure 10**: The Contact class ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image20.png))</span></span>

<span data-ttu-id="616d8-280">此時,我們創建了資料庫模型。</span><span class="sxs-lookup"><span data-stu-id="616d8-280">At this point, we have created our database model.</span></span> <span data-ttu-id="616d8-281">我們可以使用 Contact 類來表示資料庫中的特定聯繫人記錄。</span><span class="sxs-lookup"><span data-stu-id="616d8-281">We can use the Contact class to represent a particular contact record in our database.</span></span>

## <a name="creating-the-home-controller"></a><span data-ttu-id="616d8-282">建立主控制器</span><span class="sxs-lookup"><span data-stu-id="616d8-282">Creating the Home Controller</span></span>

<span data-ttu-id="616d8-283">下一步是創建我們的主控制器。</span><span class="sxs-lookup"><span data-stu-id="616d8-283">The next step is to create our Home controller.</span></span> <span data-ttu-id="616d8-284">主控制器是在 mVC 應用程式中調用的預設控制器 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="616d8-284">The Home controller is the default controller invoked in an ASP.NET MVC application.</span></span>

<span data-ttu-id="616d8-285">通過右鍵單擊解決方案資源管理器視窗中的控制器資料夾並選擇功能表選項 **「添加,控制器**」(參見圖 11),創建主控制器類。</span><span class="sxs-lookup"><span data-stu-id="616d8-285">Create the Home controller class by right-clicking the Controllers folder in the Solution Explorer window and selecting the menu option **Add, Controller** (see Figure 11).</span></span> <span data-ttu-id="616d8-286">請注意,標記為「**添加創建、更新和詳細資訊方案」操作方法的**複選框。</span><span class="sxs-lookup"><span data-stu-id="616d8-286">Notice the checkbox labeled **Add action methods for Create, Update, and Details scenarios**.</span></span> <span data-ttu-id="616d8-287">在按下「**添加**」按鈕之前,請確保選中此複選框。</span><span class="sxs-lookup"><span data-stu-id="616d8-287">Make sure that this checkbox is checked before clicking the **Add** button.</span></span>

<span data-ttu-id="616d8-288">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-288">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image11.jpg)](iteration-1-create-the-application-vb/_static/image21.png)</span></span>

<span data-ttu-id="616d8-289">**圖11**: 新增主控制器 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image22.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-289">**Figure 11**: Adding the Home controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image22.png))</span></span>

<span data-ttu-id="616d8-290">建立主控制器時,您將獲得清單 1 中的類。</span><span class="sxs-lookup"><span data-stu-id="616d8-290">When you create the Home controller, you get the class in Listing 1.</span></span>

<span data-ttu-id="616d8-291">**清單1 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="616d8-291">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample1.vb)]

## <a name="listing-the-contacts"></a><span data-ttu-id="616d8-292">列出聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-292">Listing the Contacts</span></span>

<span data-ttu-id="616d8-293">為了在"連絡人"資料庫表中顯示記錄,我們需要創建一個索引() 操作和索引視圖。</span><span class="sxs-lookup"><span data-stu-id="616d8-293">In order to display the records in the Contacts database table, we need to create an Index() action and an Index view.</span></span>

<span data-ttu-id="616d8-294">主控制器已包含索引() 操作。</span><span class="sxs-lookup"><span data-stu-id="616d8-294">The Home controller already contains an Index() action.</span></span> <span data-ttu-id="616d8-295">我們需要修改此方法,以便它看起來像清單 2。</span><span class="sxs-lookup"><span data-stu-id="616d8-295">We need to modify this method so that it looks like Listing 2.</span></span>

<span data-ttu-id="616d8-296">**清單2 - 控制器\主控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="616d8-296">**Listing 2 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample2.vb)]

<span data-ttu-id="616d8-297">請注意,清單 2 中的主控制器類\_包含名為 實體的專用欄位。</span><span class="sxs-lookup"><span data-stu-id="616d8-297">Notice that the Home controller class in Listing 2 contains a private field named \_entities.</span></span> <span data-ttu-id="616d8-298">實體\_欄位表示數據模型中的實體。</span><span class="sxs-lookup"><span data-stu-id="616d8-298">The \_entities field represents the entities from the data model.</span></span> <span data-ttu-id="616d8-299">我們使用\_實體欄位與資料庫通信。</span><span class="sxs-lookup"><span data-stu-id="616d8-299">We use the \_entities field to communicate with the database.</span></span>

<span data-ttu-id="616d8-300">Index() 方法傳回表示連絡人資料庫表中的所有聯繫人的檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-300">The Index() method returns a view that represents all of the contacts from the Contacts database table.</span></span> <span data-ttu-id="616d8-301">表達式\_實體。連絡人集.ToList() 將連絡人清單作為通用清單返回。</span><span class="sxs-lookup"><span data-stu-id="616d8-301">The expression \_entities.ContactSet.ToList() returns the list of contacts as a generic list.</span></span>

<span data-ttu-id="616d8-302">現在,我們已經創建了索引控制器,接下來我們需要創建索引視圖。</span><span class="sxs-lookup"><span data-stu-id="616d8-302">Now that we ve created the Index controller, we next need to create the Index view.</span></span> <span data-ttu-id="616d8-303">在創建索引檢視之前,請透過選擇功能表選項 **「生成、生成解決方案**」來編譯應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-303">Before creating the Index view, compile your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="616d8-304">在添加檢視之前,應始終編譯專案,以便在 **「添加檢視**」對話框中顯示模型類清單。</span><span class="sxs-lookup"><span data-stu-id="616d8-304">You should always compile your project before adding a view in order for the list of model classes to be displayed in the **Add View** dialog.</span></span>

<span data-ttu-id="616d8-305">通過右鍵單擊 Index() 方法並選擇選單選項 **「添加檢視**」來建立索引檢視(請參見圖 12)。</span><span class="sxs-lookup"><span data-stu-id="616d8-305">You create the Index view by right-clicking the Index() method and selecting the menu option **Add View** (see Figure 12).</span></span> <span data-ttu-id="616d8-306">選擇此選單選項將打開 **「添加檢視」** 對話框(參見圖 13)。</span><span class="sxs-lookup"><span data-stu-id="616d8-306">Selecting this menu option opens the **Add View** dialog (see Figure 13).</span></span>

<span data-ttu-id="616d8-307">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-307">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image12.jpg)](iteration-1-create-the-application-vb/_static/image23.png)</span></span>

<span data-ttu-id="616d8-308">**圖 12**: 新增索引檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-308">**Figure 12**: Adding the Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image24.png))</span></span>

<span data-ttu-id="616d8-309">在 **'新增檢視'** 對話框中, 選擇標籤為「**建立強類型檢視」 選單的欄位**。</span><span class="sxs-lookup"><span data-stu-id="616d8-309">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="616d8-310">選擇「查看數據類聯繫人管理器.連絡人」 和「查看內容清單」。</span><span class="sxs-lookup"><span data-stu-id="616d8-310">Select the View data class ContactManager.Contact and the View content List.</span></span> <span data-ttu-id="616d8-311">選擇這些選項將生成顯示聯繫人記錄列表的檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-311">Selecting these options generates a view that displays a list of Contact records.</span></span>

<span data-ttu-id="616d8-312">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-312">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image13.jpg)](iteration-1-create-the-application-vb/_static/image25.png)</span></span>

<span data-ttu-id="616d8-313">**圖 13**: 新增檢視對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-313">**Figure 13**: The Add View dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image26.png))</span></span>

<span data-ttu-id="616d8-314">按下「**添加**」按鈕時,將生成清單 3 中的索引檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-314">When you click the **Add** button, the Index view in Listing 3 is generated.</span></span> <span data-ttu-id="616d8-315">請注意&lt;顯示在檔案頂部&gt;的 %@ 頁 % 指令。</span><span class="sxs-lookup"><span data-stu-id="616d8-315">Notice the &lt;%@ Page %&gt; directive that appears at the top of the file.</span></span> <span data-ttu-id="616d8-316">&lt;索引檢視從ViewPage IE500"&lt;聯繫人管理器.模型.連&gt;&gt;絡人 類繼承。</span><span class="sxs-lookup"><span data-stu-id="616d8-316">The Index view inherits from the ViewPage&lt;IEnumerable&lt;ContactManager.Models.Contact&gt;&gt; class.</span></span> <span data-ttu-id="616d8-317">換句話說,視圖中的 Model 類表示聯繫人實體的清單。</span><span class="sxs-lookup"><span data-stu-id="616d8-317">In other words, the Model class in the view represents a list of Contact entities.</span></span>

<span data-ttu-id="616d8-318">Index 檢視的正文包含一個 foreach 迴圈,該迴圈通過模型類表示的每個聯繫人進行迴圈。</span><span class="sxs-lookup"><span data-stu-id="616d8-318">The body of the Index view contains a foreach loop that iterates through each of the contacts represented by the Model class.</span></span> <span data-ttu-id="616d8-319">Contact 類別的每個屬性的值顯示在 HTML 表中。</span><span class="sxs-lookup"><span data-stu-id="616d8-319">The value of each property of the Contact class is displayed within an HTML table.</span></span>

<span data-ttu-id="616d8-320">**清單 3 - 檢視\home_Index.aspx(未修改)**</span><span class="sxs-lookup"><span data-stu-id="616d8-320">**Listing 3 - Views\Home\Index.aspx (unmodified)**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample3.aspx)]

<span data-ttu-id="616d8-321">我們需要對索引視圖進行一次修改。</span><span class="sxs-lookup"><span data-stu-id="616d8-321">We need to make one modification to the Index view.</span></span> <span data-ttu-id="616d8-322">由於我們不是在創建"詳細資訊"視圖,因此我們可以刪除"詳細資訊"連結。</span><span class="sxs-lookup"><span data-stu-id="616d8-322">Because we are not creating a Details view, we can remove the Details link.</span></span> <span data-ttu-id="616d8-323">從索引檢視尋找與移除以下代碼:</span><span class="sxs-lookup"><span data-stu-id="616d8-323">Find and remove the following code from the Index view:</span></span>

<span data-ttu-id="616d8-324">{.id = 項。Id=)%&gt;</span><span class="sxs-lookup"><span data-stu-id="616d8-324">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="616d8-325">修改索引檢視後,可以運行聯繫人管理器應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-325">After you modify the Index view, you can run the Contact Manager application.</span></span> <span data-ttu-id="616d8-326">選擇功能表選項「調試」、「開始調試」或「按 F5」。</span><span class="sxs-lookup"><span data-stu-id="616d8-326">Select the menu option Debug, Start Debugging or simply press F5.</span></span> <span data-ttu-id="616d8-327">首次運行應用程式時,您將獲得圖 14 中的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="616d8-327">The first time you run the application, you get the dialog in Figure 14.</span></span> <span data-ttu-id="616d8-328">選擇 **「修改 Web.config 檔以啟用除錯**」選項,然後單擊「確定」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="616d8-328">Select the option **Modify the Web.config file to enable debugging** and click the OK button.</span></span>

<span data-ttu-id="616d8-329">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-329">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image14.jpg)](iteration-1-create-the-application-vb/_static/image27.png)</span></span>

<span data-ttu-id="616d8-330">**圖14**:啟用除錯 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image28.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-330">**Figure 14**: Enabling debugging ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image28.png))</span></span>

<span data-ttu-id="616d8-331">默認情況下,將返回索引視圖。</span><span class="sxs-lookup"><span data-stu-id="616d8-331">The Index view is returned by default.</span></span> <span data-ttu-id="616d8-332">此檢視列出聯繫人資料庫表中的所有數據(參見圖 15)。</span><span class="sxs-lookup"><span data-stu-id="616d8-332">This view lists all of the data from the Contacts database table (see Figure 15).</span></span>

<span data-ttu-id="616d8-333">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-333">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image15.jpg)](iteration-1-create-the-application-vb/_static/image29.png)</span></span>

<span data-ttu-id="616d8-334">**圖 15**: 索引檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-334">**Figure 15**: The Index view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image30.png))</span></span>

<span data-ttu-id="616d8-335">請注意,索引檢視在視圖底部包含標記為"新建"的連結。</span><span class="sxs-lookup"><span data-stu-id="616d8-335">Notice that the Index view includes a link labeled Create New at the bottom of the view.</span></span> <span data-ttu-id="616d8-336">在下一節中,您將瞭解如何創建新聯繫人。</span><span class="sxs-lookup"><span data-stu-id="616d8-336">In the next section, you learn how to create new contacts.</span></span>

## <a name="creating-new-contacts"></a><span data-ttu-id="616d8-337">建立新連絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-337">Creating New Contacts</span></span>

<span data-ttu-id="616d8-338">為了使用戶能夠創建新的聯繫人,我們需要向主控制器添加兩個 Create() 操作。</span><span class="sxs-lookup"><span data-stu-id="616d8-338">To enable users to create new contacts, we need to add two Create() actions to the Home controller.</span></span> <span data-ttu-id="616d8-339">我們需要創建一個 Create() 操作,該操作傳回 HTML 表單以創建新連絡人。</span><span class="sxs-lookup"><span data-stu-id="616d8-339">We need to create one Create() action that returns an HTML form for creating a new contact.</span></span> <span data-ttu-id="616d8-340">我們需要創建第二個 Create() 操作,以執行新聯繫人的實際資料庫插入。</span><span class="sxs-lookup"><span data-stu-id="616d8-340">We need to create a second Create() action that performs the actual database insert of the new contact.</span></span>

<span data-ttu-id="616d8-341">我們需要添加到主控制器的新 Create() 方法包含在清單 4 中。</span><span class="sxs-lookup"><span data-stu-id="616d8-341">The new Create() methods that we need to add to the Home controller are contained in Listing 4.</span></span>

<span data-ttu-id="616d8-342">**清單4 - 控制器\homeController.vb(使用建立方法)**</span><span class="sxs-lookup"><span data-stu-id="616d8-342">**Listing 4 - Controllers\HomeController.vb (with Create methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample4.vb)]

<span data-ttu-id="616d8-343">第一個 Create() 方法可以使用 HTTP GET 調用,而第二個 Create() 方法只能由 HTTP POST 調用。</span><span class="sxs-lookup"><span data-stu-id="616d8-343">The first Create() method can be invoked with an HTTP GET while the second Create() method can be invoked only by an HTTP POST.</span></span> <span data-ttu-id="616d8-344">換句話說,第二個 Create() 方法只能在發表 HTML 窗體時調用。</span><span class="sxs-lookup"><span data-stu-id="616d8-344">In other words, the second Create() method can be invoked only when posting an HTML form.</span></span> <span data-ttu-id="616d8-345">第一個 Create() 方法僅傳回包含用於創建新連絡人的 HTML 窗體的檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-345">The first Create() method simply returns a view that contains the HTML form for creating a new contact.</span></span> <span data-ttu-id="616d8-346">第二個 Create() 方法更有趣:它將新的聯繫人添加到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="616d8-346">The second Create() method is much more interesting: it adds the new contact to the database.</span></span>

<span data-ttu-id="616d8-347">請注意,已修改第二個 Create() 方法以接受 Contact 類的實例。</span><span class="sxs-lookup"><span data-stu-id="616d8-347">Notice that the second Create() method has been modified to accept an instance of the Contact class.</span></span> <span data-ttu-id="616d8-348">從 HTML 窗體發佈的表單值由 ASP.NET MVC 框架自動綁定到此 Contact 類。</span><span class="sxs-lookup"><span data-stu-id="616d8-348">The form values posted from the HTML form are bound to this Contact class by the ASP.NET MVC framework automatically.</span></span> <span data-ttu-id="616d8-349">HTML 創建表單中的每個表單欄位都分配給聯絡人「參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="616d8-349">Each form field from the HTML Create form is assigned to a property of the Contact parameter.</span></span>

<span data-ttu-id="616d8-350">請注意,連絡人參數用 [Bind] 屬性進行修飾。</span><span class="sxs-lookup"><span data-stu-id="616d8-350">Notice that the Contact parameter is decorated with a [Bind] attribute.</span></span> <span data-ttu-id="616d8-351">[綁定] 屬性用於從綁定中排除聯繫人 Id 屬性。</span><span class="sxs-lookup"><span data-stu-id="616d8-351">The [Bind] attribute is used to exclude the Contact Id property from binding.</span></span> <span data-ttu-id="616d8-352">由於 Id 屬性表示標識屬性,因此我們不希望設置 Id 屬性。</span><span class="sxs-lookup"><span data-stu-id="616d8-352">Because the Id property represents an Identity property, we don t want to set the Id property.</span></span>

<span data-ttu-id="616d8-353">在 Create() 方法的正文中,實體框架用於將新的聯繫人插入到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="616d8-353">In the body of the Create() method, the Entity Framework is used to insert the new Contact into the database.</span></span> <span data-ttu-id="616d8-354">新的連絡人將添加到現有的連絡人集,並調用 SaveChanges() 方法將這些更改推送回基礎資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-354">The new Contact is added to the existing set of Contacts and the SaveChanges() method is called to push these changes back to the underlying database.</span></span>

<span data-ttu-id="616d8-355">您可以通過右鍵按兩個 Create() 方法之一併選擇選單選項 **「新增檢視**」來生成用於創建新聯繫人的 HTML 表單(參見圖 16)。</span><span class="sxs-lookup"><span data-stu-id="616d8-355">You can generate an HTML form for creating new Contacts by right-clicking either of the two Create() methods and selecting the menu option **Add View** (see Figure 16).</span></span>

<span data-ttu-id="616d8-356">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-356">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image16.jpg)](iteration-1-create-the-application-vb/_static/image31.png)</span></span>

<span data-ttu-id="616d8-357">**圖 16**: 新增建立檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image32.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-357">**Figure 16**: Adding the Create view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image32.png))</span></span>

<span data-ttu-id="616d8-358">在 **「添加檢視」** 對話方塊中,選擇 **「連絡人管理員.連絡人」** 類別和「建立檢視內容 **」** 選項(參見圖 17)。</span><span class="sxs-lookup"><span data-stu-id="616d8-358">In the **Add View** dialog, select the **ContactManager.Contact** class and the **Create** option for view content (see Figure 17).</span></span> <span data-ttu-id="616d8-359">按下「**添加**」按鈕時,將自動生成"創建"檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-359">When you click the **Add** button, a Create view is generated automatically.</span></span>

<span data-ttu-id="616d8-360">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-360">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image17.jpg)](iteration-1-create-the-application-vb/_static/image33.png)</span></span>

<span data-ttu-id="616d8-361">**圖17**: 看到頁面爆炸 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image34.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-361">**Figure 17**: Seeing a page explode ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image34.png))</span></span>

<span data-ttu-id="616d8-362">"創建"檢視包含 Contact 類的每個屬性的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="616d8-362">The Create view contains form fields for each of the properties of the Contact class.</span></span> <span data-ttu-id="616d8-363">"創建"檢視的代碼包含在清單 5 中。</span><span class="sxs-lookup"><span data-stu-id="616d8-363">The code for the Create view is included in Listing 5.</span></span>

<span data-ttu-id="616d8-364">**清單 5 - 檢視\home_Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="616d8-364">**Listing 5 - Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample5.aspx)]

<span data-ttu-id="616d8-365">修改 Create() 方法並添加"創建"視圖後,可以運行連絡人經理應用程式並創建新連絡人。</span><span class="sxs-lookup"><span data-stu-id="616d8-365">After you modify the Create() methods and add the Create view, you can run the Contact Manger application and create new contacts.</span></span> <span data-ttu-id="616d8-366">按下「**新建**」檢視中顯示的連結以導航到「創建」檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-366">Click the **Create New** link that appears in the Index view to navigate to the Create view.</span></span> <span data-ttu-id="616d8-367">您應該在圖 18 中看到檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-367">You should see the view in Figure 18.</span></span>

<span data-ttu-id="616d8-368">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-368">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image18.jpg)](iteration-1-create-the-application-vb/_static/image35.png)</span></span>

<span data-ttu-id="616d8-369">**圖 18**: 建立檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image36.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-369">**Figure 18**: The Create View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image36.png))</span></span>

## <a name="editing-contacts"></a><span data-ttu-id="616d8-370">編輯聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-370">Editing Contacts</span></span>

<span data-ttu-id="616d8-371">添加用於編輯連絡人記錄的功能與添加創建新連絡人記錄的功能非常相似。</span><span class="sxs-lookup"><span data-stu-id="616d8-371">Adding the functionality for editing a contact record is very similar to adding the functionality for creating new contact records.</span></span> <span data-ttu-id="616d8-372">首先,我們需要向主控制器類添加兩種新的 Edit 方法。</span><span class="sxs-lookup"><span data-stu-id="616d8-372">First, we need to add two new Edit methods to the Home controller class.</span></span> <span data-ttu-id="616d8-373">這些新的 Edit() 方法包含在清單 6 中。</span><span class="sxs-lookup"><span data-stu-id="616d8-373">These new Edit() methods are contained in Listing 6.</span></span>

<span data-ttu-id="616d8-374">**清單6 - 控制器\主控制器.vb(使用編輯方法)**</span><span class="sxs-lookup"><span data-stu-id="616d8-374">**Listing 6 - Controllers\HomeController.vb (with Edit methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample6.vb)]

<span data-ttu-id="616d8-375">第一個 Edit() 方法由 HTTP GET 操作調用。</span><span class="sxs-lookup"><span data-stu-id="616d8-375">The first Edit() method is invoked by an HTTP GET operation.</span></span> <span data-ttu-id="616d8-376">Id 參數傳遞給此方法,此方法表示要編輯的聯繫人記錄的 ID。</span><span class="sxs-lookup"><span data-stu-id="616d8-376">An Id parameter is passed to this method which represents the Id of the contact record being edited.</span></span> <span data-ttu-id="616d8-377">實體框架用於檢索與 Id 匹配的連絡人。返回包含用於編輯記錄的 HTML 窗體的檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-377">The Entity Framework is used to retrieve a contact that matches the Id. A view that contains an HTML form for editing a record is returned.</span></span>

<span data-ttu-id="616d8-378">第二個 Edit() 方法執行對資料庫的實際更新。</span><span class="sxs-lookup"><span data-stu-id="616d8-378">The second Edit() method performs the actual update to the database.</span></span> <span data-ttu-id="616d8-379">此方法接受 Contact 類的實例作為參數。</span><span class="sxs-lookup"><span data-stu-id="616d8-379">This method accepts an instance of the Contact class as a parameter.</span></span> <span data-ttu-id="616d8-380">ASP.NET MVC 框架會自動將表單欄位從「編輯」窗體綁定到此類。</span><span class="sxs-lookup"><span data-stu-id="616d8-380">The ASP.NET MVC framework binds the form fields from the Edit form to this class automatically.</span></span> <span data-ttu-id="616d8-381">請注意,在編輯連絡人時,您沒有包含 [Bind] 屬性(我們需要 Id 屬性的值)。</span><span class="sxs-lookup"><span data-stu-id="616d8-381">Notice that you don t include the[Bind] attribute when editing a Contact (we need the value of the Id property).</span></span>

<span data-ttu-id="616d8-382">實體框架用於將修改後的聯繫人保存到資料庫。</span><span class="sxs-lookup"><span data-stu-id="616d8-382">The Entity Framework is used to save the modified Contact to the database.</span></span> <span data-ttu-id="616d8-383">必須首先從資料庫中檢索原始聯繫人。</span><span class="sxs-lookup"><span data-stu-id="616d8-383">The original Contact must be retrieved from the database first.</span></span> <span data-ttu-id="616d8-384">接下來,調用實體框架應用屬性更改() 方法來記錄對聯繫人的更改。</span><span class="sxs-lookup"><span data-stu-id="616d8-384">Next, the Entity Framework ApplyPropertyChanges() method is called to record the changes to the Contact.</span></span> <span data-ttu-id="616d8-385">最後,調用實體框架保存更改() 方法來保留對基礎資料庫的更改。</span><span class="sxs-lookup"><span data-stu-id="616d8-385">Finally, the Entity Framework SaveChanges() method is called to persist the changes to the underlying database.</span></span>

<span data-ttu-id="616d8-386">您可以通過右鍵按一下 Edit() 方法並選擇選單選項「添加檢視」來生成包含「編輯」窗體的視圖。</span><span class="sxs-lookup"><span data-stu-id="616d8-386">You can generate the view that contains the Edit form by right-clicking the Edit() method and selecting the menu option Add View.</span></span> <span data-ttu-id="616d8-387">在"添加檢視"對話框中,選擇 **"連絡人管理器.模型.聯繫人類"** 和 **「編輯**檢視」內容(參見圖 19)。</span><span class="sxs-lookup"><span data-stu-id="616d8-387">In the Add View dialog, select the **ContactManager.Models.Contact** class and the **Edit** view content (see Figure 19).</span></span>

<span data-ttu-id="616d8-388">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-388">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image19.jpg)](iteration-1-create-the-application-vb/_static/image37.png)</span></span>

<span data-ttu-id="616d8-389">**圖 19**: 新增編輯檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image38.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-389">**Figure 19**: Adding an Edit View ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image38.png))</span></span>

<span data-ttu-id="616d8-390">按下「添加」按鈕時,將自動生成新的「編輯」檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-390">When you click the Add button, a new Edit view is generated automatically.</span></span> <span data-ttu-id="616d8-391">生成的 HTML 窗體包含對應於 Contact 類的每個屬性的欄位(請參見清單 7)。</span><span class="sxs-lookup"><span data-stu-id="616d8-391">The HTML form that is generated contains fields that correspond to each of the properties of the Contact class (see Listing 7).</span></span>

<span data-ttu-id="616d8-392">**清單7 - 檢視\home_編輯.aspx**</span><span class="sxs-lookup"><span data-stu-id="616d8-392">**Listing 7 - Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample7.aspx)]

## <a name="deleting-contacts"></a><span data-ttu-id="616d8-393">移除聯絡人</span><span class="sxs-lookup"><span data-stu-id="616d8-393">Deleting Contacts</span></span>

<span data-ttu-id="616d8-394">如果要刪除連絡人,則需要向主控制器類添加兩個 Delete() 操作。</span><span class="sxs-lookup"><span data-stu-id="616d8-394">If you want to delete contacts then you need to add two Delete() actions to the Home controller class.</span></span> <span data-ttu-id="616d8-395">第一個刪除() 操作顯示刪除確認表單。</span><span class="sxs-lookup"><span data-stu-id="616d8-395">The first Delete() action displays a delete confirmation form.</span></span> <span data-ttu-id="616d8-396">第二個 Delete() 操作執行實際刪除。</span><span class="sxs-lookup"><span data-stu-id="616d8-396">The second Delete() action performs the actual delete.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="616d8-397">稍後,在反覆運算#7中,我們修改聯繫人管理器,以便它支援 Ajax 刪除的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="616d8-397">Later, in Iteration #7, we modify the Contact Manager so that it supports a one step Ajax delete.</span></span>

<span data-ttu-id="616d8-398">清單8中包含兩種新的 Delete() 方法。</span><span class="sxs-lookup"><span data-stu-id="616d8-398">The two new Delete() methods are contained in Listing 8.</span></span>

<span data-ttu-id="616d8-399">**清單8 - 控制器\主控制器.vb(刪除方法)**</span><span class="sxs-lookup"><span data-stu-id="616d8-399">**Listing 8 - Controllers\HomeController.vb (Delete methods)**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample8.vb)]

<span data-ttu-id="616d8-400">第一個 Delete() 方法傳回一個確認表單,用於從資料庫中刪除連絡人記錄(參見圖 20)。</span><span class="sxs-lookup"><span data-stu-id="616d8-400">The first Delete() method returns a confirmation form for deleting a contact record from the database (see Figure20).</span></span> <span data-ttu-id="616d8-401">第二個 Delete() 方法對資料庫執行實際刪除操作。</span><span class="sxs-lookup"><span data-stu-id="616d8-401">The second Delete() method performs the actual delete operation against the database.</span></span> <span data-ttu-id="616d8-402">從資料庫檢索原始連絡人後,將調用實體框架 DeleteObject() 和保存更改()方法以執行資料庫刪除。</span><span class="sxs-lookup"><span data-stu-id="616d8-402">After the original contact has been retrieved from the database, the Entity Framework DeleteObject() and SaveChanges() methods are called to perform the database delete.</span></span>

<span data-ttu-id="616d8-403">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-403">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image20.jpg)](iteration-1-create-the-application-vb/_static/image39.png)</span></span>

<span data-ttu-id="616d8-404">**圖20**:刪除確認檢視([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-404">**Figure 20**: The delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image40.png))</span></span>

<span data-ttu-id="616d8-405">我們需要修改 Index 檢視,以便它包含用於刪除聯繫人記錄的連結(參見圖 21)。</span><span class="sxs-lookup"><span data-stu-id="616d8-405">We need to modify the Index view so that it contains a link for deleting contact records (see Figure 21).</span></span> <span data-ttu-id="616d8-406">您需要將以下代碼加入包含「編輯」連結的同一表單元格中:</span><span class="sxs-lookup"><span data-stu-id="616d8-406">You need to add the following code to the same table cell that contains the Edit link:</span></span>

<span data-ttu-id="616d8-407">{.id = 項。Id=)%&gt;</span><span class="sxs-lookup"><span data-stu-id="616d8-407">{.id = item.Id})%&gt;</span></span>

<span data-ttu-id="616d8-408">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-408">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image21.jpg)](iteration-1-create-the-application-vb/_static/image41.png)</span></span>

<span data-ttu-id="616d8-409">**圖21**:索引檢視與編輯連結([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image42.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-409">**Figure 21**: Index view with Edit link ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image42.png))</span></span>

<span data-ttu-id="616d8-410">接下來,我們需要創建刪除確認檢視。</span><span class="sxs-lookup"><span data-stu-id="616d8-410">Next, we need to create the delete confirmation view.</span></span> <span data-ttu-id="616d8-411">右鍵按一下主控制器類中的 Delete() 方法,然後選擇選單選項「添加視圖」。</span><span class="sxs-lookup"><span data-stu-id="616d8-411">Right-click the Delete() method in the Home controller class and select the menu option Add View.</span></span> <span data-ttu-id="616d8-412">將顯示「添加檢視」對話框(參見圖 22)。</span><span class="sxs-lookup"><span data-stu-id="616d8-412">The Add View dialog appears (see Figure 22).</span></span>

<span data-ttu-id="616d8-413">與「清單」、"創建「和」編輯「檢視」的情況不同,「添加檢視」對話框不包含創建「刪除」檢視的選項。</span><span class="sxs-lookup"><span data-stu-id="616d8-413">Unlike in the case of the List, Create, and Edit views, the Add View dialog does not contain an option to create a Delete view.</span></span> <span data-ttu-id="616d8-414">而是選擇 **「聯繫人管理器.模型.連絡人**資料類」和 **「空**檢視」內容。</span><span class="sxs-lookup"><span data-stu-id="616d8-414">Instead, select the **ContactManager.Models.Contact** data class and the **Empty** view content.</span></span> <span data-ttu-id="616d8-415">選擇"空檢視內容"選項需要我們自己創建視圖。</span><span class="sxs-lookup"><span data-stu-id="616d8-415">Selecting the Empty view content option will require us to create the view ourselves.</span></span>

<span data-ttu-id="616d8-416">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-416">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image22.jpg)](iteration-1-create-the-application-vb/_static/image43.png)</span></span>

<span data-ttu-id="616d8-417">**圖22**:新增刪除確認檢視 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image44.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-417">**Figure 22**: Adding the delete confirmation view ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image44.png))</span></span>

<span data-ttu-id="616d8-418">"刪除"檢視的內容包含在清單 9 中。</span><span class="sxs-lookup"><span data-stu-id="616d8-418">The content of the Delete view is contained in Listing 9.</span></span> <span data-ttu-id="616d8-419">此檢視包含一個表單,該窗體確認是否應刪除特定聯繫人(參見圖 21)。</span><span class="sxs-lookup"><span data-stu-id="616d8-419">This view contains a form that confirms whether or not a particular contact should be deleted (see Figure 21).</span></span>

<span data-ttu-id="616d8-420">**清單 9 - 檢視\home_Delete.aspx**</span><span class="sxs-lookup"><span data-stu-id="616d8-420">**Listing 9 - Views\Home\Delete.aspx**</span></span>

[!code-aspx[Main](iteration-1-create-the-application-vb/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a><span data-ttu-id="616d8-421">變更預設控制器名稱</span><span class="sxs-lookup"><span data-stu-id="616d8-421">Changing the Name of the Default Controller</span></span>

<span data-ttu-id="616d8-422">使用聯絡人的控制器類的名稱名為 HomeController 類,這可能會讓您煩惱。</span><span class="sxs-lookup"><span data-stu-id="616d8-422">It might bother you that the name of our controller class for working with contacts is named the HomeController class.</span></span> <span data-ttu-id="616d8-423">控制器不應被命名為「連絡人控制器」?</span><span class="sxs-lookup"><span data-stu-id="616d8-423">Shouldn't the controller be named ContactController?</span></span>

<span data-ttu-id="616d8-424">此問題很容易解決。</span><span class="sxs-lookup"><span data-stu-id="616d8-424">This issue is easy enough to fix.</span></span> <span data-ttu-id="616d8-425">首先,我們需要重構主控制器的名稱。</span><span class="sxs-lookup"><span data-stu-id="616d8-425">First, we need to refactor the name of the Home controller.</span></span> <span data-ttu-id="616d8-426">在 Visual Studio 代碼編輯器中打開 HomeController 類,右鍵單擊類的名稱並選擇選單選項 **「重命名**」。</span><span class="sxs-lookup"><span data-stu-id="616d8-426">Open the HomeController class in the Visual Studio Code Editor, right click the name of the class and select the menu option **Rename**.</span></span> <span data-ttu-id="616d8-427">選擇此選單選項將打開" 重新命名對話框。</span><span class="sxs-lookup"><span data-stu-id="616d8-427">Selecting this menu option opens the Rename dialog.</span></span>

<span data-ttu-id="616d8-428">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-428">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image23.jpg)](iteration-1-create-the-application-vb/_static/image45.png)</span></span>

<span data-ttu-id="616d8-429">**圖23**:重構控制器名稱 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image46.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-429">**Figure 23**: Refactoring a controller name ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image46.png))</span></span>

<span data-ttu-id="616d8-430">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-430">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image24.jpg)](iteration-1-create-the-application-vb/_static/image47.png)</span></span>

<span data-ttu-id="616d8-431">**圖24**:使用重新命名對話框 ([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image48.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-431">**Figure 24**: Using the Rename dialog ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image48.png))</span></span>

<span data-ttu-id="616d8-432">如果重新命名控制器類,Visual Studio 也會更新「檢視」資料夾中資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="616d8-432">If you rename your controller class, Visual Studio will update the name of the folder in the Views folder as well.</span></span> <span data-ttu-id="616d8-433">Visual Studio 會將 [視圖]主頁資料夾重命名為 [視圖]連絡人資料夾。</span><span class="sxs-lookup"><span data-stu-id="616d8-433">Visual Studio will rename the \Views\Home folder to the \Views\Contact folder.</span></span>

<span data-ttu-id="616d8-434">進行此更改後,應用程式將不再具有主控制器。</span><span class="sxs-lookup"><span data-stu-id="616d8-434">After you make this change, your application will no longer have a Home controller.</span></span> <span data-ttu-id="616d8-435">執行應用程式時,您將獲得圖 25 中的錯誤頁。</span><span class="sxs-lookup"><span data-stu-id="616d8-435">When you run your application, you'll get the error page in Figure 25.</span></span>

<span data-ttu-id="616d8-436">[![[New Project] \(新增專案\) 對話方塊](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span><span class="sxs-lookup"><span data-stu-id="616d8-436">[![The New Project dialog box](iteration-1-create-the-application-vb/_static/image25.jpg)](iteration-1-create-the-application-vb/_static/image49.png)</span></span>

<span data-ttu-id="616d8-437">**圖25:** 無預設控制器([按下以檢視全尺寸影像](iteration-1-create-the-application-vb/_static/image50.png))</span><span class="sxs-lookup"><span data-stu-id="616d8-437">**Figure 25**: No default controller ([Click to view full-size image](iteration-1-create-the-application-vb/_static/image50.png))</span></span>

<span data-ttu-id="616d8-438">我們需要更新 Global.asax 檔案中的預設路由,以便使用聯繫人控制器而不是主控制器。</span><span class="sxs-lookup"><span data-stu-id="616d8-438">We need to update the default route in the Global.asax file to use the Contact controller instead of the Home controller.</span></span> <span data-ttu-id="616d8-439">打開 Global.asax 檔並修改預設路由使用的預設控制器(請參見清單 10)。</span><span class="sxs-lookup"><span data-stu-id="616d8-439">Open the Global.asax file and modify the default controller used by the default route (see Listing 10).</span></span>

<span data-ttu-id="616d8-440">**清單10 - 全域.asax.vb**</span><span class="sxs-lookup"><span data-stu-id="616d8-440">**Listing 10 - Global.asax.vb**</span></span>

[!code-vb[Main](iteration-1-create-the-application-vb/samples/sample10.vb)]

<span data-ttu-id="616d8-441">進行這些更改後,聯繫人管理器將正確運行。</span><span class="sxs-lookup"><span data-stu-id="616d8-441">After you make these changes, the Contact Manager will run correctly.</span></span> <span data-ttu-id="616d8-442">現在,它將使用聯繫人控制器類作為默認控制器。</span><span class="sxs-lookup"><span data-stu-id="616d8-442">Now, it will use the Contact controller class as the default controller.</span></span>

## <a name="summary"></a><span data-ttu-id="616d8-443">總結</span><span class="sxs-lookup"><span data-stu-id="616d8-443">Summary</span></span>

<span data-ttu-id="616d8-444">在第一次反覆運算中,我們以盡可能快的方式創建了一個基本的聯繫人管理器應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-444">In this first iteration, we created a basic Contact Manager application in the fastest way possible.</span></span> <span data-ttu-id="616d8-445">我們利用 Visual Studio 自動為控制器和檢視生成初始代碼。</span><span class="sxs-lookup"><span data-stu-id="616d8-445">We took advantage of Visual Studio to generate the initial code for our controllers and views automatically.</span></span> <span data-ttu-id="616d8-446">我們還利用實體框架自動生成資料庫模型類。</span><span class="sxs-lookup"><span data-stu-id="616d8-446">We also took advantage of the Entity Framework to generate our database model classes automatically.</span></span>

<span data-ttu-id="616d8-447">目前,我們可以使用聯繫人管理器應用程式列出、創建、編輯和刪除聯繫人記錄。</span><span class="sxs-lookup"><span data-stu-id="616d8-447">Currently, we can list, create, edit, and delete contact records with the Contact Manager application.</span></span> <span data-ttu-id="616d8-448">換句話說,我們可以執行資料庫驅動的 Web 應用程式所需的所有基本資料庫操作。</span><span class="sxs-lookup"><span data-stu-id="616d8-448">In other words, we can perform all of the basic database operations required by a database-driven web application.</span></span>

<span data-ttu-id="616d8-449">不幸的是,我們的應用程式有一些問題。</span><span class="sxs-lookup"><span data-stu-id="616d8-449">Unfortunately, our application has some problems.</span></span> <span data-ttu-id="616d8-450">首先,我猶豫地承認這一點,聯繫人管理器應用程式不是最有吸引力的應用程式。</span><span class="sxs-lookup"><span data-stu-id="616d8-450">First and I hesitate to admit this, the Contact Manager application is not the most attractive application.</span></span> <span data-ttu-id="616d8-451">它需要一些設計工作。</span><span class="sxs-lookup"><span data-stu-id="616d8-451">It needs some design work.</span></span> <span data-ttu-id="616d8-452">在下一次反覆運算中,我們將瞭解如何更改默認視圖母版頁和級聯樣式表,以改善應用程序的外觀。</span><span class="sxs-lookup"><span data-stu-id="616d8-452">In the next iteration, we'll look at how we can change the default view master page and cascading style sheet to improve the appearance of the application.</span></span>

<span data-ttu-id="616d8-453">其次,我們尚未實現任何表單驗證。</span><span class="sxs-lookup"><span data-stu-id="616d8-453">Second, we have not implemented any form validation.</span></span> <span data-ttu-id="616d8-454">例如,沒有任何措施可以阻止您提交"創建連絡人表單",而無需為任何表單欄位輸入值。</span><span class="sxs-lookup"><span data-stu-id="616d8-454">For example, there is nothing to prevent you from submitting the Create contact form without entering values for any of the form fields.</span></span> <span data-ttu-id="616d8-455">此外,您還可以輸入無效的電話號碼和電子郵寄地址。</span><span class="sxs-lookup"><span data-stu-id="616d8-455">Furthermore, you can enter invalid phone numbers and email addresses.</span></span> <span data-ttu-id="616d8-456">我們開始在反覆運算#3解決表單驗證問題。</span><span class="sxs-lookup"><span data-stu-id="616d8-456">We start to tackle the problem of form validation in iteration #3.</span></span>

<span data-ttu-id="616d8-457">最後,最重要的是,無法輕鬆修改或維護聯繫人管理器應用程式的當前反覆運算。</span><span class="sxs-lookup"><span data-stu-id="616d8-457">Finally, and most importantly, the current iteration of the Contact Manager application cannot be easily modified or maintained.</span></span> <span data-ttu-id="616d8-458">例如,資料庫訪問邏輯直接烘焙到控制器操作中。</span><span class="sxs-lookup"><span data-stu-id="616d8-458">For example, the database access logic is baked right into the controller actions.</span></span> <span data-ttu-id="616d8-459">這意味著,如果不修改控制器,我們就無法修改數據訪問代碼。</span><span class="sxs-lookup"><span data-stu-id="616d8-459">This means that we cannot modify our data access code without modifying our controllers.</span></span> <span data-ttu-id="616d8-460">在以後的反覆運算中,我們探索了可以實現的軟體設計模式,以使聯繫人管理器對更改更具彈性。</span><span class="sxs-lookup"><span data-stu-id="616d8-460">In later iterations, we explore software design patterns that we can implement to make the Contact Manager more resilient to change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="616d8-461">[前一個](iteration-7-add-ajax-functionality-cs.md)
> [下一個](iteration-2-make-the-application-look-nice-vb.md)</span><span class="sxs-lookup"><span data-stu-id="616d8-461">[Previous](iteration-7-add-ajax-functionality-cs.md)
[Next](iteration-2-make-the-application-look-nice-vb.md)</span></span>
