---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: 反覆運算#6 = 使用測試驅動開發 (VB) |微軟文件
author: rick-anderson
description: 在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。 在此反覆運算中,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 8464f4cdee673ef75d561e4cf89613fdca2c16af
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542803"
---
# <a name="iteration-6--use-test-driven-development-vb"></a><span data-ttu-id="7ee9e-104">反覆項目 #6 – 使用測試導向的開發 (VB)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-104">Iteration #6 – Use test-driven development (VB)</span></span>

<span data-ttu-id="7ee9e-105">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7ee9e-106">下載代碼</span><span class="sxs-lookup"><span data-stu-id="7ee9e-106">Download Code</span></span>](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> <span data-ttu-id="7ee9e-107">在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7ee9e-108">在此反覆運算中,我們添加聯繫人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-108">In this iteration, we add contact groups.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="7ee9e-109">建構 MVC 應用程式 (VB) ASP.NET連絡人管理</span><span class="sxs-lookup"><span data-stu-id="7ee9e-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="7ee9e-110">在本系列教程中,我們從頭到尾構建整個聯繫人管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="7ee9e-111">透過聯絡人管理員應用程式,您可以儲存連絡人資訊 (姓名、電話號碼和電子郵件位址) 人員清單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="7ee9e-112">我們通過多次反覆運算構建應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="7ee9e-113">每次反覆運算時,我們都會逐步改進應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="7ee9e-114">此多反覆運算方法的目標是使您能夠瞭解每次更改的原因。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="7ee9e-115">反覆運算#1 - 創建應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="7ee9e-116">在第一次反覆運算中,我們以最簡單的方式創建聯繫人管理器。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="7ee9e-117">我們添加對基本資料庫操作的支援:創建、讀取、更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="7ee9e-118">反覆運算#2 - 使應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="7ee9e-119">在此反覆運算中,我們通過修改預設ASP.NET MVC 檢視母版頁和級聯樣式表來改進應用程式的外觀。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="7ee9e-120">反覆運算#3 - 添加表單驗證。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="7ee9e-121">在第三個反覆運算中,我們添加基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="7ee9e-122">我們防止人們在未填寫所需表單欄位的情況下提交表單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="7ee9e-123">我們還驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="7ee9e-124">反覆運算#4 - 使應用程式鬆散耦合。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="7ee9e-125">在第四次反覆運算中,我們利用多種軟體設計模式,使維護和修改聯繫人管理器應用程式變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="7ee9e-126">例如,我們重構應用程式以使用存儲庫模式和依賴項注入模式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="7ee9e-127">反覆運算#5 - 創建單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="7ee9e-128">在第五次反覆運算中,我們通過添加單元測試使應用程式更易於維護和修改。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="7ee9e-129">我們類比數據模型類,並為控制器和驗證邏輯構建單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="7ee9e-130">反覆運算#6 - 使用測試驅動開發。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="7ee9e-131">在第六次反覆運算中,我們首先編寫單元測試並針對單元測試編寫代碼,從而向應用程式添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7ee9e-132">在此反覆運算中,我們添加聯繫人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="7ee9e-133">反覆運算#7 - 添加Ajax功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="7ee9e-134">在第七次反覆運算中,我們通過增加對Ajax的支援來提高應用程式的回應性和性能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="7ee9e-135">此反覆運算</span><span class="sxs-lookup"><span data-stu-id="7ee9e-135">This Iteration</span></span>

<span data-ttu-id="7ee9e-136">在 Contact Manager 應用程式的上一次反覆運算中,我們創建了單元測試,為我們的代碼提供一個安全網。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="7ee9e-137">創建單元測試的動機是使我們的代碼對更改更具彈性。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="7ee9e-138">通過單元測試,我們可以愉快地對我們的代碼進行任何更改,並立即知道我們是否破壞了現有功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="7ee9e-139">在此反覆運算中,我們將單元測試用於完全不同的目的。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="7ee9e-140">在此反覆運算中,我們將單元測試用作稱為*測試驅動開發*的應用程式設計理念的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="7ee9e-141">練習測試驅動開發時,首先編寫測試,然後針對測試編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="7ee9e-142">更確切地說,在練習測試驅動開發時,在創建代碼時完成三個步驟(紅色/綠色/重構):</span><span class="sxs-lookup"><span data-stu-id="7ee9e-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="7ee9e-143">編寫失敗的單元測試(紅色)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="7ee9e-144">編寫通過單元測試的代碼(綠色)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="7ee9e-145">重構代碼(重構)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="7ee9e-146">首先,編寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-146">First, you write the unit test.</span></span> <span data-ttu-id="7ee9e-147">單元測試應表達您希望代碼如何的行為的意圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="7ee9e-148">首次創建單元測試時,單元測試應失敗。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="7ee9e-149">測試應失敗,因為您尚未編寫滿足測試的任何應用程式代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="7ee9e-150">接下來,您只編寫足夠的代碼,以便單元測試通過。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="7ee9e-151">目標是以最懶、最懶、最快的方式編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="7ee9e-152">不應浪費時間考慮應用程式的體系結構。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="7ee9e-153">相反,您應該專注於編寫滿足單元測試表達的意圖所需的最小代碼量。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="7ee9e-154">最後,在編寫了足夠的代碼后,您可以退後一步考慮應用程式的整體體系結構。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="7ee9e-155">在此步驟中,您利用軟體設計模式(如儲存庫模式)重寫(重構)代碼,以便代碼更可維護。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="7ee9e-156">您可以在此步驟中無所畏懼地重寫代碼,因為單元測試涵蓋了您的代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="7ee9e-157">實踐測試驅動開發會帶來許多好處。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="7ee9e-158">首先,測試驅動的開發迫使您專注於實際需要編寫的代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="7ee9e-159">由於您始終專注於編寫足夠的代碼以通過特定的測試,因此您無法遊蕩到雜草中,並編寫大量永遠不會使用的代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="7ee9e-160">其次,「測試第一」設計方法迫使您從如何使用代碼的角度編寫代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="7ee9e-161">換句話說,在練習測試驅動開發時,您會不斷從使用者的角度編寫測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="7ee9e-162">因此,測試驅動的開發可以產生更清潔、更易懂的 API。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="7ee9e-163">最後,測試驅動的開發迫使您編寫單元測試,作為編寫應用程式的正常過程的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="7ee9e-164">隨著專案截止時間的臨近,測試通常是視窗外的第一件事。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="7ee9e-165">另一方面,在實踐測試驅動開發時,您更有可能對編寫單元測試具有道德性,因為測試驅動開發使單元測試成為構建應用程式過程的核心。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7ee9e-166">要瞭解有關測試驅動開發的更多內容,我建議您閱讀 Michael Feathers 的書,**以有效使用舊代碼**。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>

<span data-ttu-id="7ee9e-167">在此反覆運算中,我們將向聯繫人管理器應用程式添加新功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="7ee9e-168">我們添加對聯繫人組的支援。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-168">We add support for Contact Groups.</span></span> <span data-ttu-id="7ee9e-169">您可以使用"連絡人組"將聯絡人組織到"業務"和"朋友"組等類別中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="7ee9e-170">我們將遵循測試驅動開發過程,將這項新功能添加到我們的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="7ee9e-171">我們將首先編寫單元測試,並針對這些測試編寫所有代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="7ee9e-172">測試內容</span><span class="sxs-lookup"><span data-stu-id="7ee9e-172">What Gets Tested</span></span>

<span data-ttu-id="7ee9e-173">正如我們在上一次反覆運算中討論的那樣,您通常不會為數據訪問邏輯或視圖邏輯編寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="7ee9e-174">您不會為資料訪問邏輯編寫單元測試,因為訪問資料庫的操作相對較慢。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="7ee9e-175">您不為檢視邏輯編寫單元測試,因為造訪檢視需要旋轉 Web 伺服器,這是一個相對較慢的操作。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="7ee9e-176">除非測試可以快速一遍又一遍地執行,否則不應編寫單元測試</span><span class="sxs-lookup"><span data-stu-id="7ee9e-176">You shouldn't write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="7ee9e-177">由於測試驅動開發由單元測試驅動,所以我們最初側重於編寫控制器和業務邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="7ee9e-178">我們避免觸摸資料庫或視圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-178">We avoid touching the database or views.</span></span> <span data-ttu-id="7ee9e-179">在本教程結束之前,我們不會修改資料庫或創建視圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-179">We won't modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="7ee9e-180">我們從可以測試的內容開始。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="7ee9e-181">建立使用者情景</span><span class="sxs-lookup"><span data-stu-id="7ee9e-181">Creating User Stories</span></span>

<span data-ttu-id="7ee9e-182">練習測試驅動開發時,您總是從編寫測試開始。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="7ee9e-183">這立即提出了一個問題:你如何決定先寫什麼測試?</span><span class="sxs-lookup"><span data-stu-id="7ee9e-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="7ee9e-184">要回答這個問題,你應該編寫一組[*使用者情景*](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-184">To answer this question, you should write a set of [*user stories*](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="7ee9e-185">使用者情景是軟體要求的非常簡短(通常是一個句子)描述。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="7ee9e-186">它應該是從使用者的角度編寫的對需求的非技術描述。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="7ee9e-187">以下是描述新的聯絡人群組功能所需的功能的使用者情景集:</span><span class="sxs-lookup"><span data-stu-id="7ee9e-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="7ee9e-188">使用者可以查看連絡人組的清單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="7ee9e-189">用戶可以創建新的連絡人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="7ee9e-190">用戶可以刪除現有的連絡人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="7ee9e-191">創建新連絡人時,用戶可以選擇連絡人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="7ee9e-192">用戶可以在編輯現有聯繫人時選擇連絡人組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="7ee9e-193">連絡人組清單顯示在「索引」檢視中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="7ee9e-194">當用戶按一下連絡人組時,將顯示匹配連絡人的清單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="7ee9e-195">請注意,客戶完全可以理解此使用者情景清單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="7ee9e-196">沒有提到技術實施細節。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="7ee9e-197">在構建應用程式的過程中,使用者情景集可能會變得更加精細。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="7ee9e-198">您可以將使用者情景分解為多個情景(要求)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="7ee9e-199">例如,您可能決定創建新的聯繫人組應涉及驗證。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="7ee9e-200">提交沒有名稱的聯繫人組應返回驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="7ee9e-201">創建使用者情景清單后,即可編寫第一個單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="7ee9e-202">我們將首先創建用於查看聯繫人組列表的單位測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="7ee9e-203">列出聯絡人群組</span><span class="sxs-lookup"><span data-stu-id="7ee9e-203">Listing Contact Groups</span></span>

<span data-ttu-id="7ee9e-204">我們的第一個使用者故事是,用戶應該能夠查看聯繫人組的清單。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="7ee9e-205">我們需要用測試來表達這個故事。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-205">We need to express this story with a test.</span></span>

<span data-ttu-id="7ee9e-206">通過右鍵單擊 ContactManager.測試專案中的控制器資料夾、選擇 **「添加、新建測試**」並選擇單元測試範本來創建新**的單元測試**(參見圖 1)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="7ee9e-207">命名新的單元測試組ControllerTest.vb,然後單擊 **「確定**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-207">Name the new unit test GroupControllerTest.vb and click the **OK** button.</span></span>

<span data-ttu-id="7ee9e-208">[![新增組控制器測試單元測試](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span></span>

<span data-ttu-id="7ee9e-209">**圖 01**: 新增群組控制器測試單元測試([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image2.png))</span></span>

<span data-ttu-id="7ee9e-210">我們的第一個單元測試包含在清單 1 中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="7ee9e-211">此測試驗證組控制器的 Index() 方法是否傳回一組群組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="7ee9e-212">測試驗證在檢視數據中返回組的集合。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="7ee9e-213">**清單 1 - 控制器\群組控制器測試.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

<span data-ttu-id="7ee9e-214">當您首次在 Visual Studio 中鍵入清單 1 中的代碼時,您將獲得大量紅色波浪線。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="7ee9e-215">我們尚未創建組控制器或組類。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="7ee9e-216">此時,我們甚至不能構建應用程式,因此無法執行第一個單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="7ee9e-217">很好</span><span class="sxs-lookup"><span data-stu-id="7ee9e-217">That s good.</span></span> <span data-ttu-id="7ee9e-218">這算作一個失敗的測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-218">That counts as a failing test.</span></span> <span data-ttu-id="7ee9e-219">因此,我們現在有權開始編寫應用程式代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="7ee9e-220">我們需要編寫足夠的代碼來執行我們的測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="7ee9e-221">清單 2 中的組控制器類包含通過單元測試所需的最小代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="7ee9e-222">Index() 操作傳回靜態編碼的群組清單(組類在清單 3 中定義)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="7ee9e-223">**清單2 - 控制器\群組控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-223">**Listing 2 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

<span data-ttu-id="7ee9e-224">**清單3 - 模型_Group.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-224">**Listing 3 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

<span data-ttu-id="7ee9e-225">將 GroupController 和組類添加到專案中後,我們的第一個單元測試將成功完成(參見圖 2)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="7ee9e-226">我們已經做了通過考試所需的最低工作。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="7ee9e-227">是時候慶祝了。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-227">It is time to celebrate.</span></span>

<span data-ttu-id="7ee9e-228">[![成功!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span></span>

<span data-ttu-id="7ee9e-229">**圖02:** 成功!([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image4.png))</span></span>

## <a name="creating-contact-groups"></a><span data-ttu-id="7ee9e-230">建立聯絡人群組</span><span class="sxs-lookup"><span data-stu-id="7ee9e-230">Creating Contact Groups</span></span>

<span data-ttu-id="7ee9e-231">現在,我們可以轉到第二個使用者情景。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="7ee9e-232">我們需要能夠創建新的聯繫組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="7ee9e-233">我們需要用測試來表達這個意圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="7ee9e-234">清單4中的測試驗證,使用新組調用 Create() 方法會將組添加到 Index() 方法傳回的組清單中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="7ee9e-235">換句話說,如果我創建了一個新組,那麼我應該能夠從 Index() 方法返回的組列表中恢復新組。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="7ee9e-236">**清單4 - 控制器\組控制器測試.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

<span data-ttu-id="7ee9e-237">清單4中的測試使用新的聯繫人組調用組控制器 Create() 方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="7ee9e-238">接下來,測試驗證調用組控制器 Index() 方法返回檢視中的新組數據。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="7ee9e-239">清單 5 中修改後的組控制器包含透過新測試所需的最小變更。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="7ee9e-240">**清單5 - 控制器\群組控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-240">**Listing 5 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="7ee9e-241">清單 5 中的組控制器具有新的 Create() 操作。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="7ee9e-242">此操作將組添加到組的集合中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="7ee9e-243">請注意,已修改 Index() 操作以返回組集合的內容。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="7ee9e-244">再次,我們執行了通過單元測試所需的最低工作量。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="7ee9e-245">對組控制器進行這些更改后,所有單元測試都通過。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="7ee9e-246">新增驗證</span><span class="sxs-lookup"><span data-stu-id="7ee9e-246">Adding Validation</span></span>

<span data-ttu-id="7ee9e-247">在使用者情景中未明確說明此要求。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="7ee9e-248">但是,要求集團有名稱是合理的。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="7ee9e-249">否則,將聯繫人組織到組中將不是很有用。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="7ee9e-250">清單6包含表示此意圖的新測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="7ee9e-251">此測試驗證嘗試創建組而不提供名稱會導致模型狀態的驗證錯誤消息。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="7ee9e-252">**清單6 - 控制器\組控制器測試.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

<span data-ttu-id="7ee9e-253">為了滿足此測試,我們需要向組類添加 Name 屬性(請參閱清單 7)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="7ee9e-254">此外,我們需要向組控制器的 Create() 操作添加一點驗證邏輯(參見清單 8)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="7ee9e-255">**清單7 - 模型_Group.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-255">**Listing 7 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

<span data-ttu-id="7ee9e-256">**清單8 - 控制器\群組控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-256">**Listing 8 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

<span data-ttu-id="7ee9e-257">請注意,組控制器 Create() 操作現在同時包含驗證和資料庫邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="7ee9e-258">目前,組控制器使用的資料庫僅包含記憶體中的集合。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="7ee9e-259">重構時間</span><span class="sxs-lookup"><span data-stu-id="7ee9e-259">Time to Refactor</span></span>

<span data-ttu-id="7ee9e-260">紅色/綠色/重構的第三步是重構部分。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="7ee9e-261">此時,我們需要從代碼中退後一步,考慮如何重構應用程式以改進其設計。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="7ee9e-262">重構階段是我們認真思考實現軟體設計原則和模式的最佳方式的階段。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="7ee9e-263">我們可以自由地修改我們的代碼,我們選擇以任何方式改進代碼的設計。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="7ee9e-264">我們有一個單元測試安全網,以防止我們破壞現有功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="7ee9e-265">現在,從良好的軟體設計來看,我們的集團控制器是一團糟。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="7ee9e-266">組控制器包含一堆的驗證和數據訪問代碼。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="7ee9e-267">為了避免違反單一責任原則,我們需要將這些關注分為不同的類別。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="7ee9e-268">我們的重構組控制器類包含在清單 9 中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="7ee9e-269">控制器已修改為使用 ContactManager 服務層。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="7ee9e-270">這與我們與聯繫人控制器一起使用的服務層相同。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="7ee9e-271">清單10包含添加到 ContactManager 服務層以支援驗證、列出和創建組的新方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="7ee9e-272">IContactManager 服務介面已更新,以包括新方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="7ee9e-273">清單11包含一個新的FakeContactManagerManager儲存庫類,該類實現了IContactManagerRepository介面。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="7ee9e-274">與同時實現 IContactManager Repository 介面的實體聯繫人管理器儲存庫類不同,我們新的 FakeContactManagerManager Repository 類不與資料庫通信。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="7ee9e-275">FakeContactManagerManagerRepository 類使用記憶體中集合作為資料庫的代理。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="7ee9e-276">我們將在單元測試中將此類用作假存儲庫層。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="7ee9e-277">**清單9 - 控制器\群組控制器.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-277">**Listing 9 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

<span data-ttu-id="7ee9e-278">**清單 10 - 控制器\連絡管理員服務.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-278">**Listing 10 - Controllers\ContactManagerService.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

<span data-ttu-id="7ee9e-279">**清單11 - 控制器\假連絡人管理員儲存庫.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]

<span data-ttu-id="7ee9e-280">修改 IContactManager 儲存庫介面需要用於在實體連絡人管理員儲存庫類別中實現 CreateGroup() 和清單組()方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="7ee9e-281">最懶惰和最快的方法是添加如下所示的存根方法:</span><span class="sxs-lookup"><span data-stu-id="7ee9e-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]

<span data-ttu-id="7ee9e-282">最後,對應用程式設計的這些更改要求我們對單元測試進行一些修改。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="7ee9e-283">現在,在執行單元測試時,我們需要使用假聯繫人管理器存儲庫。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="7ee9e-284">更新後的 GroupControllerTest 類包含在清單 12 中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="7ee9e-285">**清單12 - 控制器\組控制器測試.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

<span data-ttu-id="7ee9e-286">在我們進行所有這些更改后,我們再次通過所有單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="7ee9e-287">我們已經完成了整個紅色/綠色/重構週期。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="7ee9e-288">我們已經實現了前兩個使用者情景。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="7ee9e-289">現在,我們支持使用者情景中表達的要求單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="7ee9e-290">實現其餘使用者情景涉及重複相同的紅色/綠色/重構週期。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="7ee9e-291">變更資料庫</span><span class="sxs-lookup"><span data-stu-id="7ee9e-291">Modifying our Database</span></span>

<span data-ttu-id="7ee9e-292">不幸的是,儘管我們滿足了單元測試表達的所有要求,但我們的工作並沒有完成。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="7ee9e-293">我們仍然需要修改我們的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-293">We still need to modify our database.</span></span>

<span data-ttu-id="7ee9e-294">我們需要創建新的組資料庫表。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-294">We need to create a new Group database table.</span></span> <span data-ttu-id="7ee9e-295">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ee9e-295">Follow these steps:</span></span>

1. <span data-ttu-id="7ee9e-296">在「伺服器資源管理器」視窗中,右鍵按一下「表」資料夾並選擇功能表選項 **「添加新表**」。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="7ee9e-297">輸入下表設計器中描述的兩列。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="7ee9e-298">將 Id 列標記為主鍵和標識列。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="7ee9e-299">按下軟碟的圖示,保存具有名稱組的新錶。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.12_table01"></a>

| <span data-ttu-id="7ee9e-300">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-300">**Column Name**</span></span> | <span data-ttu-id="7ee9e-301">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-301">**Data Type**</span></span> | <span data-ttu-id="7ee9e-302">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ee9e-303">Id</span><span class="sxs-lookup"><span data-stu-id="7ee9e-303">Id</span></span> | <span data-ttu-id="7ee9e-304">int</span><span class="sxs-lookup"><span data-stu-id="7ee9e-304">int</span></span> | <span data-ttu-id="7ee9e-305">False</span><span class="sxs-lookup"><span data-stu-id="7ee9e-305">False</span></span> |
| <span data-ttu-id="7ee9e-306">名稱</span><span class="sxs-lookup"><span data-stu-id="7ee9e-306">Name</span></span> | <span data-ttu-id="7ee9e-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-307">nvarchar(50)</span></span> | <span data-ttu-id="7ee9e-308">False</span><span class="sxs-lookup"><span data-stu-id="7ee9e-308">False</span></span> |

<span data-ttu-id="7ee9e-309">接下來,我們需要從"連絡人"表中刪除所有資料(否則,我們將無法在"連絡人"和"組"表之間創建關係)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won't be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="7ee9e-310">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ee9e-310">Follow these steps:</span></span>

1. <span data-ttu-id="7ee9e-311">右鍵按兩下"連絡人"表並選擇功能表選項 **"顯示表數據**"。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="7ee9e-312">刪除所有行。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-312">Delete all of the rows.</span></span>

<span data-ttu-id="7ee9e-313">接下來,我們需要定義組資料庫表和現有聯繫人資料庫表之間的關係。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="7ee9e-314">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ee9e-314">Follow these steps:</span></span>

1. <span data-ttu-id="7ee9e-315">按兩下伺服器資源管理器視窗中的"連絡人"表以打開表設計器。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="7ee9e-316">向名為 GroupId 的"連絡人"表添加新整數列。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="7ee9e-317">按下「關係」按鈕以打開「外鍵關係」對話框(參見圖 3)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="7ee9e-318">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-318">Click the Add button.</span></span>
5. <span data-ttu-id="7ee9e-319">按下「表和列規範」按鈕旁邊的省略號按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="7ee9e-320">在"表和列"對話框中,選擇組作為主鍵表,選擇 Id 作為主鍵列。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="7ee9e-321">選擇"連絡人"作為外鍵表,將 GroupId 作為外鍵列(參見圖 4)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="7ee9e-322">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-322">Click the OK button.</span></span>
7. <span data-ttu-id="7ee9e-323">在 **'插入"和"更新規範"** 下,選擇**刪除規則**的值 **「級聯**」。。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="7ee9e-324">按下「關閉」按鈕以關閉「外鍵關係」對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="7ee9e-325">按下「儲存」按鈕將更改儲存到"連絡人"表。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-325">Click the Save button to save the changes to the Contacts table.</span></span>

<span data-ttu-id="7ee9e-326">[![建立資料庫表關係](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span></span>

<span data-ttu-id="7ee9e-327">**圖 03**: 建立資料庫表關係([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image6.png))</span></span>

<span data-ttu-id="7ee9e-328">[![指定表關係](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-328">[![Specifying table relationships](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span></span>

<span data-ttu-id="7ee9e-329">**圖 04**:指定表格([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image8.png))</span></span>

### <a name="updating-our-data-model"></a><span data-ttu-id="7ee9e-330">更新資料模型</span><span class="sxs-lookup"><span data-stu-id="7ee9e-330">Updating our Data Model</span></span>

<span data-ttu-id="7ee9e-331">接下來,我們需要更新數據模型以表示新的資料庫表。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="7ee9e-332">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7ee9e-332">Follow these steps:</span></span>

1. <span data-ttu-id="7ee9e-333">按兩下「模型」資料夾中的 ContactManagerModel.edmx 檔以打開實體設計器。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="7ee9e-334">右鍵按一下「設計器」曲面,然後從資料庫中選擇功能表選項 **「更新模型**」。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="7ee9e-335">在"更新嚮導"中,選擇"組"表並按兩下"完成"按鈕(參見圖 5)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="7ee9e-336">右鍵按一下「組實體」並選擇功能表選項 **「重新命名**」。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="7ee9e-337">將*組*實體的名稱更改為*組*(單數)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="7ee9e-338">右鍵按一下顯示在「聯繫人」實體底部的「組導航屬性」。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="7ee9e-339">將*組*導航屬性的名稱更改為*組*(單數)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>

<span data-ttu-id="7ee9e-340">[![從資料庫更新實體框架模型](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span></span>

<span data-ttu-id="7ee9e-341">**圖 05**:從資料庫更新實體框架模型([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image10.png))</span></span>

<span data-ttu-id="7ee9e-342">完成這些步驟后,數據模型將同時表示"聯繫人"和"組"表。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="7ee9e-343">實體設計器應顯示兩個實體(參見圖 6)。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-343">The Entity Designer should show both entities (see Figure 6).</span></span>

<span data-ttu-id="7ee9e-344">[![實體設計器顯示群組與聯絡人](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span></span>

<span data-ttu-id="7ee9e-345">**圖 06**: 實體設計器顯示群組與聯絡人([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image12.png))</span></span>

### <a name="creating-our-repository-classes"></a><span data-ttu-id="7ee9e-346">建立我們的儲存庫類別</span><span class="sxs-lookup"><span data-stu-id="7ee9e-346">Creating our Repository Classes</span></span>

<span data-ttu-id="7ee9e-347">接下來,我們需要實現我們的存儲庫類。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="7ee9e-348">在此反覆運算過程中,我們在編寫代碼以滿足單元測試的同時,向IContactManagerRepository介面添加了幾種新方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="7ee9e-349">IContactManager儲存庫介面的最終版本包含在清單14中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="7ee9e-350">**清單 14 - 型號\IContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-350">**Listing 14 - Models\IContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

<span data-ttu-id="7ee9e-351">我們實際上尚未實現與在真實實體聯繫人管理器存儲庫類中使用聯繫人組相關的任何方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-351">We haven't actually implemented any of the methods related to working with contact groups in our real EntityContactManagerRepository class.</span></span> <span data-ttu-id="7ee9e-352">目前,實體聯繫人管理體儲存庫類具有IContactManagerRepository介面中列出的每個連絡人組方法的存根方法。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="7ee9e-353">例如,ListGroups() 方法目前如下所示:</span><span class="sxs-lookup"><span data-stu-id="7ee9e-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

<span data-ttu-id="7ee9e-354">存根方法使我們能夠編譯應用程式並通過單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="7ee9e-355">但是,現在是時候實際實現這些方法了。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="7ee9e-356">實體聯繫人管理器儲存庫類的最終版本包含在清單 13 中。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="7ee9e-357">**清單13 - 模型_實體連絡人管理員儲存庫.vb**</span><span class="sxs-lookup"><span data-stu-id="7ee9e-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a><span data-ttu-id="7ee9e-358">建立檢視</span><span class="sxs-lookup"><span data-stu-id="7ee9e-358">Creating the Views</span></span>

<span data-ttu-id="7ee9e-359">使用預設ASP.NET檢視引擎時,ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="7ee9e-360">因此,您不會創建檢視以回應特定的單元測試。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="7ee9e-361">但是,由於沒有檢視的應用程式將毫無用處,因此,如果不創建和修改 Contact Manager 應用程式中的視圖,我們就無法完成此反覆運算。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="7ee9e-362">我們需要建立以下用於管理連絡人組的新檢視(參見圖 7):</span><span class="sxs-lookup"><span data-stu-id="7ee9e-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="7ee9e-363">檢視_組\索引.aspx - 顯示聯絡人群組清單</span><span class="sxs-lookup"><span data-stu-id="7ee9e-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="7ee9e-364">檢視\組\刪除.aspx - 顯示用於刪除聯絡人群組的確認表單</span><span class="sxs-lookup"><span data-stu-id="7ee9e-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>

<span data-ttu-id="7ee9e-365">[![群組索引檢視](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-365">[![The Group Index view](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span></span>

<span data-ttu-id="7ee9e-366">**圖 07**: 群組索引檢視([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image14.png))</span></span>

<span data-ttu-id="7ee9e-367">我們需要修改以下現有檢視,以便它們包括聯絡人組:</span><span class="sxs-lookup"><span data-stu-id="7ee9e-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="7ee9e-368">檢視\Home_Create.aspx</span><span class="sxs-lookup"><span data-stu-id="7ee9e-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="7ee9e-369">檢視\首頁\編輯.aspx</span><span class="sxs-lookup"><span data-stu-id="7ee9e-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="7ee9e-370">檢視\首頁\索引.aspx</span><span class="sxs-lookup"><span data-stu-id="7ee9e-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="7ee9e-371">通過查看本教程附帶的 Visual Studio 應用程式,可以查看修改後的檢視。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="7ee9e-372">例如,圖 8 說明瞭聯繫人索引視圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-372">For example, Figure 8 illustrates the Contact Index view.</span></span>

<span data-ttu-id="7ee9e-373">[![連絡人索引檢視](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-373">[![The Contact Index view](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span></span>

<span data-ttu-id="7ee9e-374">**圖 08**: 連絡人索引檢視([按下以檢視全尺寸影像](iteration-6-use-test-driven-development-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="7ee9e-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image16.png))</span></span>

## <a name="summary"></a><span data-ttu-id="7ee9e-375">總結</span><span class="sxs-lookup"><span data-stu-id="7ee9e-375">Summary</span></span>

<span data-ttu-id="7ee9e-376">在此反覆運算中,我們遵循測試驅動的開發應用程式設計方法,向 Contact Manager 應用程式添加了新功能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="7ee9e-377">我們首先創建一組使用者情景。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="7ee9e-378">我們創建了一組單元測試,這些測試對應於使用者情景表達的要求。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="7ee9e-379">最後,我們編寫的代碼足夠滿足單元測試表達的要求。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="7ee9e-380">完成編寫足夠的代碼以滿足單元測試表達的要求后,我們更新了資料庫和視圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="7ee9e-381">我們將新的組表添加到我們的資料庫中,並更新了實體框架數據模型。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="7ee9e-382">我們還創建並修改了一組視圖。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="7ee9e-383">在下一次反覆運算(最後反覆運算)中,我們重寫應用程式以利用Ajax。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="7ee9e-384">通過使用Ajax,我們將提高聯繫人管理器應用程式的回應性和性能。</span><span class="sxs-lookup"><span data-stu-id="7ee9e-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ee9e-385">[前一個](iteration-5-create-unit-tests-vb.md)
> [下一個](iteration-7-add-ajax-functionality-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7ee9e-385">[Previous](iteration-5-create-unit-tests-vb.md)
[Next](iteration-7-add-ajax-functionality-vb.md)</span></span>
