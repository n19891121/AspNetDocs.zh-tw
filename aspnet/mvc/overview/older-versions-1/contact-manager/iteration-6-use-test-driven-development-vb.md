---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: '反覆項目 #6 – 使用測試導向開發 (VB) |Microsoft Docs'
author: microsoft
description: 在這個第六個反覆項目中，我們新功能加入我們的應用程式方法是先撰寫單元測試，並撰寫單元測試的程式碼。 在此反覆項目，...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 3fd252b94e55f02215a2733f218e68b26486691f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59397106"
---
# <a name="iteration-6--use-test-driven-development-vb"></a><span data-ttu-id="35984-104">反覆項目 #6 – 使用測試導向開發 (VB)</span><span class="sxs-lookup"><span data-stu-id="35984-104">Iteration #6 – Use test-driven development (VB)</span></span>

<span data-ttu-id="35984-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="35984-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="35984-106">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="35984-106">Download Code</span></span>](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> <span data-ttu-id="35984-107">在這個第六個反覆項目中，我們新功能加入我們的應用程式方法是先撰寫單元測試，並撰寫單元測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="35984-108">在這個反覆項目，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="35984-108">In this iteration, we add contact groups.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="35984-109">建立連絡人管理 ASP.NET MVC 應用程式 (VB)</span><span class="sxs-lookup"><span data-stu-id="35984-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="35984-110">在本系列教學課程中，我們會建置整個連絡人管理應用程式從開始到完成。</span><span class="sxs-lookup"><span data-stu-id="35984-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="35984-111">請連絡系統管理員應用程式可讓您商店連絡資訊的名稱、 電話號碼和電子郵件地址-的人員清單。</span><span class="sxs-lookup"><span data-stu-id="35984-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="35984-112">我們會建置應用程式透過多個反覆項目。</span><span class="sxs-lookup"><span data-stu-id="35984-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="35984-113">每次反覆運算時，我們會逐漸改善應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="35984-114">此多個反覆項目方法的目標是要讓您了解每個變更的原因。</span><span class="sxs-lookup"><span data-stu-id="35984-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="35984-115">反覆項目 #1-建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="35984-116">在第一次反覆運算中，我們建立連絡人管理員中的最簡單的方式可能。</span><span class="sxs-lookup"><span data-stu-id="35984-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="35984-117">我們將新增基本資料庫作業的支援：建立、 讀取、 更新和刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="35984-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="35984-118">反覆項目 #2-讓應用程式看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="35984-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="35984-119">這個反覆項目，我們以改善應用程式的外觀的修改預設的 ASP.NET MVC 檢視主版頁面和階層式樣式表。</span><span class="sxs-lookup"><span data-stu-id="35984-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="35984-120">反覆項目 #3-新增表單驗證。</span><span class="sxs-lookup"><span data-stu-id="35984-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="35984-121">在第三個反覆項目，我們會加入基本表單驗證。</span><span class="sxs-lookup"><span data-stu-id="35984-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="35984-122">我們可以防止使用者提交表單，而不會完成必要的表單欄位。</span><span class="sxs-lookup"><span data-stu-id="35984-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="35984-123">此外，我們也會驗證電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="35984-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="35984-124">反覆項目 #4-進行鬆散偶合的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="35984-125">在這個第四個反覆項目中，我們利用數種軟體設計模式，以讓它更容易維護及修改連絡人管理員應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="35984-126">比方說，我們可以重構應用程式使用儲存機制模式和相依性插入模式。</span><span class="sxs-lookup"><span data-stu-id="35984-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="35984-127">反覆項目 #5-建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="35984-128">在第五個反覆項目中，我們讓我們的應用程式容易維護及修改藉由新增單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="35984-129">我們模擬我們的資料模型類別，並建置我們的控制器和驗證邏輯單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="35984-130">反覆項目 #6-使用測試導向開發。</span><span class="sxs-lookup"><span data-stu-id="35984-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="35984-131">在這個第六個反覆項目中，我們新功能加入我們的應用程式方法是先撰寫單元測試，並撰寫單元測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="35984-132">在這個反覆項目，我們會新增連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="35984-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="35984-133">反覆項目 #7-新增 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="35984-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="35984-134">在第七個反覆項目，改善回應性和我們的應用程式的效能透過新增對 Ajax 支援。</span><span class="sxs-lookup"><span data-stu-id="35984-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="35984-135">這個反覆項目</span><span class="sxs-lookup"><span data-stu-id="35984-135">This Iteration</span></span>

<span data-ttu-id="35984-136">在連絡人管理員應用程式的上一個反覆項目，我們會建立單元測試，以提供我們的程式碼防護機制。</span><span class="sxs-lookup"><span data-stu-id="35984-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="35984-137">用於建立單元測試的動機是讓我們的程式碼變更更有彈性。</span><span class="sxs-lookup"><span data-stu-id="35984-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="35984-138">使用就地的單元測試，我們可以值得高興的是我們的程式碼進行任何變更，並立即了解我們的電腦已中斷的現有功能。</span><span class="sxs-lookup"><span data-stu-id="35984-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="35984-139">這個反覆項目，在中，我們會使用單元測試完全不同的用途。</span><span class="sxs-lookup"><span data-stu-id="35984-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="35984-140">在這個反覆項目，我們會使用單元測試做為一部分的呼叫的應用程式的設計原理*測試導向開發*。</span><span class="sxs-lookup"><span data-stu-id="35984-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="35984-141">當您將練習測試導向開發時，您會先撰寫測試，並再撰寫測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="35984-142">更精確地說，當練習測試導向開發，有三個步驟完成時建立的程式碼 (紅色 / 綠色/重構):</span><span class="sxs-lookup"><span data-stu-id="35984-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="35984-143">撰寫單元測試失敗 （紅色）</span><span class="sxs-lookup"><span data-stu-id="35984-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="35984-144">撰寫程式碼，通過單元測試 （綠色）</span><span class="sxs-lookup"><span data-stu-id="35984-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="35984-145">重構程式碼 (Refactor)</span><span class="sxs-lookup"><span data-stu-id="35984-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="35984-146">首先，您可以撰寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-146">First, you write the unit test.</span></span> <span data-ttu-id="35984-147">單元測試應該表達您打算如您預期您的程式碼如何運作。</span><span class="sxs-lookup"><span data-stu-id="35984-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="35984-148">當您第一次建立單元測試時，單元測試應該會失敗。</span><span class="sxs-lookup"><span data-stu-id="35984-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="35984-149">測試應該會失敗，因為但是尚未寫入測試任何應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="35984-150">接下來，您可以撰寫剛好足夠的程式碼以便將單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="35984-151">目標是 laziest、 sloppiest 又最快速的可能方式撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="35984-152">您應該不會浪費時間來思考您的應用程式的架構。</span><span class="sxs-lookup"><span data-stu-id="35984-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="35984-153">相反地，您應該專注於撰寫少量的程式碼不必滿足單元測試所表示的意圖。</span><span class="sxs-lookup"><span data-stu-id="35984-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="35984-154">最後，您已撰寫足夠的程式碼之後，您可以回頭考慮您的應用程式的整體架構。</span><span class="sxs-lookup"><span data-stu-id="35984-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="35984-155">在此步驟中，重寫 (refactor) 您的程式碼利用軟體設計模式-儲存機制模式-例如，讓您的程式碼更容易維護。</span><span class="sxs-lookup"><span data-stu-id="35984-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="35984-156">您可以放心地請重寫您的程式碼，在此步驟中因為單元測試所涵蓋的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="35984-157">有許多因練習測試導向開發的許多優點。</span><span class="sxs-lookup"><span data-stu-id="35984-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="35984-158">首先，以測試為導向的開發會強迫您專注於真正需要撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="35984-159">因為您經常會著重於只撰寫不足，無法將特定測試的程式碼，您無法從踏入檢討和寫入大量您永遠不會使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="35984-160">其次，「 第一次測試 」 的設計方法會強制您撰寫程式碼從您的程式碼的使用方式觀點來看。</span><span class="sxs-lookup"><span data-stu-id="35984-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="35984-161">換句話說，當練習測試導向開發，您要從使用者觀點不斷地撰寫測試。</span><span class="sxs-lookup"><span data-stu-id="35984-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="35984-162">因此，測試導向開發可能會導致更簡潔且更容易了解的 Api。</span><span class="sxs-lookup"><span data-stu-id="35984-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="35984-163">最後，測試導向開發也會強迫您撰寫單元測試做為撰寫的應用程式的一般程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="35984-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="35984-164">隨著專案期限將近，測試是通常會在視窗第一件事。</span><span class="sxs-lookup"><span data-stu-id="35984-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="35984-165">當練習測試導向開發，相反地，您會更有可能是良性的相關撰寫單元測試，因為測試導向開發對單元測試集中建置的應用程式的程序。</span><span class="sxs-lookup"><span data-stu-id="35984-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="35984-166">若要深入了解測試導向開發，建議您閱讀 Michael Feathers 書籍**Working Effectively with Legacy 程式碼**。</span><span class="sxs-lookup"><span data-stu-id="35984-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>


<span data-ttu-id="35984-167">在此反覆項目，我們新增連絡人管理員應用程式的新功能。</span><span class="sxs-lookup"><span data-stu-id="35984-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="35984-168">我們新增連絡人群組的支援。</span><span class="sxs-lookup"><span data-stu-id="35984-168">We add support for Contact Groups.</span></span> <span data-ttu-id="35984-169">您可以使用連絡人群組，以將您的連絡人組織成類別目錄，例如業務和 Friend 群組。</span><span class="sxs-lookup"><span data-stu-id="35984-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="35984-170">我們將新增至應用程式的這項新功能，依照測試導向開發的程序。</span><span class="sxs-lookup"><span data-stu-id="35984-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="35984-171">我們將先撰寫我們的單元測試，我們將撰寫所有我們針對這些測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="35984-172">接受測試的基準</span><span class="sxs-lookup"><span data-stu-id="35984-172">What Gets Tested</span></span>

<span data-ttu-id="35984-173">如我們所討論的上一個反覆項目，您通常不撰寫資料存取邏輯的單元測試或檢視邏輯。</span><span class="sxs-lookup"><span data-stu-id="35984-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="35984-174">您不針對資料存取邏輯的 t 寫入單元測試，因為存取資料庫的相對比較慢的作業。</span><span class="sxs-lookup"><span data-stu-id="35984-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="35984-175">因為存取檢視需要加速作業相當緩慢的 web 伺服器，您可以不檢視邏輯的 t 寫入單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="35984-176">除非可以執行測試一再重複速度非常快，您不應該撰寫的單元測試</span><span class="sxs-lookup"><span data-stu-id="35984-176">You shouldn't write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="35984-177">因為測試為導向的開發由單元測試，則我們一開始專注於撰寫控制站和商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="35984-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="35984-178">我們避免碰觸的資料庫或檢視表。</span><span class="sxs-lookup"><span data-stu-id="35984-178">We avoid touching the database or views.</span></span> <span data-ttu-id="35984-179">我們不會修改資料庫，或者建立我們的檢視，直到本教學課程中的最尾端。</span><span class="sxs-lookup"><span data-stu-id="35984-179">We won't modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="35984-180">我們開始項目可進行測試。</span><span class="sxs-lookup"><span data-stu-id="35984-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="35984-181">建立使用者劇本</span><span class="sxs-lookup"><span data-stu-id="35984-181">Creating User Stories</span></span>

<span data-ttu-id="35984-182">當練習測試導向開發，您一律從開始撰寫測試。</span><span class="sxs-lookup"><span data-stu-id="35984-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="35984-183">這會立即引發問題：您要如何決定先撰寫哪些測試？</span><span class="sxs-lookup"><span data-stu-id="35984-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="35984-184">為了回答這個問題，您應該撰寫一組[*使用者劇本*](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="35984-184">To answer this question, you should write a set of [*user stories*](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="35984-185">使用者劇本是非常短暫的軟體需求 （通常是一個句子） 描述。</span><span class="sxs-lookup"><span data-stu-id="35984-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="35984-186">它應該是非技術性需求，從使用者觀點來看撰寫的描述。</span><span class="sxs-lookup"><span data-stu-id="35984-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="35984-187">以下說明新的連絡人群組功能所需的功能的使用者劇本的集合：</span><span class="sxs-lookup"><span data-stu-id="35984-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="35984-188">使用者可以檢視連絡人群組的清單。</span><span class="sxs-lookup"><span data-stu-id="35984-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="35984-189">使用者可以建立新的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="35984-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="35984-190">使用者可以刪除現有的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="35984-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="35984-191">建立新的連絡人時，使用者可以選取連絡人的群組。</span><span class="sxs-lookup"><span data-stu-id="35984-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="35984-192">編輯現有的連絡人時，使用者可以選取連絡人的群組。</span><span class="sxs-lookup"><span data-stu-id="35984-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="35984-193">連絡人的群組清單會顯示在 [索引] 檢視中。</span><span class="sxs-lookup"><span data-stu-id="35984-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="35984-194">當使用者按一下連絡人群組時，則會顯示相符的連絡人的清單。</span><span class="sxs-lookup"><span data-stu-id="35984-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="35984-195">請注意，此清單中的使用者劇本客戶完全理解。</span><span class="sxs-lookup"><span data-stu-id="35984-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="35984-196">沒有任何值得一提的技術實作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="35984-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="35984-197">而在建置您的應用程式，使用者劇本的集合可能會變得更精細。</span><span class="sxs-lookup"><span data-stu-id="35984-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="35984-198">您可能會分成多個劇本 （需求） 的使用者劇本。</span><span class="sxs-lookup"><span data-stu-id="35984-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="35984-199">例如，您可能決定建立新的連絡人群組應該包含驗證。</span><span class="sxs-lookup"><span data-stu-id="35984-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="35984-200">提交連絡人群組沒有名稱應該會傳回驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="35984-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="35984-201">您建立的使用者劇本清單之後，您就可以開始撰寫第一個單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="35984-202">我們先建立檢視的 連絡人群組清單的單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="35984-203">清單連絡人的群組</span><span class="sxs-lookup"><span data-stu-id="35984-203">Listing Contact Groups</span></span>

<span data-ttu-id="35984-204">我們的第一個使用者劇本是使用者應該能夠檢視連絡人群組的清單。</span><span class="sxs-lookup"><span data-stu-id="35984-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="35984-205">我們需要表達此劇本與測試。</span><span class="sxs-lookup"><span data-stu-id="35984-205">We need to express this story with a test.</span></span>

<span data-ttu-id="35984-206">建立新的單元測試，以滑鼠右鍵按一下 [控制器] 資料夾，在 ContactManager.Tests 專案中，選取**新增]、 [新增測試**，然後選取**單元測試**範本 （見 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="35984-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="35984-207">名稱，新的單元測試 GroupControllerTest.vb，然後按一下**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="35984-207">Name the new unit test GroupControllerTest.vb and click the **OK** button.</span></span>


<span data-ttu-id="35984-208">[![新增 GroupControllerTest 單元測試](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35984-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span></span>

<span data-ttu-id="35984-209">**圖 01**:新增 GroupControllerTest 單元測試 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="35984-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image2.png))</span></span>


<span data-ttu-id="35984-210">第一個單元測試會包含在程式碼範例 1。</span><span class="sxs-lookup"><span data-stu-id="35984-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="35984-211">此測試會驗證群組控制器的 index （） 方法會傳回一組群組。</span><span class="sxs-lookup"><span data-stu-id="35984-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="35984-212">測試會驗證，群組就會傳回集合檢視中的資料。</span><span class="sxs-lookup"><span data-stu-id="35984-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="35984-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

<span data-ttu-id="35984-214">當您第一次輸入程式碼，在 Visual Studio 中的列表 1 中時，您會取得大量的紅色曲線。</span><span class="sxs-lookup"><span data-stu-id="35984-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="35984-215">我們不會建立 GroupController 或群組的類別。</span><span class="sxs-lookup"><span data-stu-id="35984-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="35984-216">到目前為止，我們可以 t 甚至建置我們的應用程式讓我們可以 t 執行的第一個單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="35984-217">該良好的 s。</span><span class="sxs-lookup"><span data-stu-id="35984-217">That s good.</span></span> <span data-ttu-id="35984-218">會被視為失敗的測試。</span><span class="sxs-lookup"><span data-stu-id="35984-218">That counts as a failing test.</span></span> <span data-ttu-id="35984-219">因此，我們現在有開始撰寫應用程式程式碼的權限。</span><span class="sxs-lookup"><span data-stu-id="35984-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="35984-220">我們必須撰寫足夠執行我們的測試的程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="35984-221">在 列表 2 中的群組控制器類別包含通過單元測試所需的程式碼的最低限度。</span><span class="sxs-lookup"><span data-stu-id="35984-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="35984-222">Index （） 動作傳回靜態程式碼的清單 （群組類別定義在 列表 3） 的群組。</span><span class="sxs-lookup"><span data-stu-id="35984-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="35984-223">**Listing 2 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-223">**Listing 2 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

<span data-ttu-id="35984-224">**列表 3-Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-224">**Listing 3 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

<span data-ttu-id="35984-225">我們將 GroupController 和群組類別新增至我們的專案之後，第一個單元測試成功完成 （請參閱 圖 2）。</span><span class="sxs-lookup"><span data-stu-id="35984-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="35984-226">我們已經通過測試所需的最小工作。</span><span class="sxs-lookup"><span data-stu-id="35984-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="35984-227">它是要慶祝的時間。</span><span class="sxs-lookup"><span data-stu-id="35984-227">It is time to celebrate.</span></span>


<span data-ttu-id="35984-228">[![成功 ！](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="35984-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span></span>

<span data-ttu-id="35984-229">**圖 02**:成功 ！([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="35984-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image4.png))</span></span>


## <a name="creating-contact-groups"></a><span data-ttu-id="35984-230">建立連絡人群組</span><span class="sxs-lookup"><span data-stu-id="35984-230">Creating Contact Groups</span></span>

<span data-ttu-id="35984-231">現在我們可以移至第二個使用者劇本。</span><span class="sxs-lookup"><span data-stu-id="35984-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="35984-232">我們必須要能夠建立新的連絡人群組。</span><span class="sxs-lookup"><span data-stu-id="35984-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="35984-233">我們需要與測試 express 這個意圖。</span><span class="sxs-lookup"><span data-stu-id="35984-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="35984-234">列表 4 中的測試會驗證呼叫 create （） 方法，以新的群組將群組加入到 index （） 方法所傳回的群組清單。</span><span class="sxs-lookup"><span data-stu-id="35984-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="35984-235">換句話說，如果我建立新的群組然後我應該能夠從 index （） 方法所傳回的群組清單取得新的群組。</span><span class="sxs-lookup"><span data-stu-id="35984-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="35984-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

<span data-ttu-id="35984-237">列表 4 中的測試會呼叫的群組控制站與新的連絡人群組的 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="35984-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="35984-238">接下來，測試會驗證檢視資料，呼叫群組控制器 index （） 方法會傳回新的群組。</span><span class="sxs-lookup"><span data-stu-id="35984-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="35984-239">列表 5 中已修改的群組控制站會包含最低限度將新的測試所需的變更。</span><span class="sxs-lookup"><span data-stu-id="35984-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="35984-240">**Listing 5 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-240">**Listing 5 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="35984-241">表 5 中的群組控制站會有一個新的 create （） 動作。</span><span class="sxs-lookup"><span data-stu-id="35984-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="35984-242">此動作會將群組加入群組的集合。</span><span class="sxs-lookup"><span data-stu-id="35984-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="35984-243">請注意，已修改的 index （） 動作来傳回的群組集合的內容。</span><span class="sxs-lookup"><span data-stu-id="35984-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="35984-244">同樣地，我們可以執行通過單元測試所需的最低限度。</span><span class="sxs-lookup"><span data-stu-id="35984-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="35984-245">我們的群組控制站進行這些變更之後，所有我們的單元測試成功。</span><span class="sxs-lookup"><span data-stu-id="35984-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="35984-246">新增驗證</span><span class="sxs-lookup"><span data-stu-id="35984-246">Adding Validation</span></span>

<span data-ttu-id="35984-247">在 使用者劇本，是不明確陳述這項需求。</span><span class="sxs-lookup"><span data-stu-id="35984-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="35984-248">不過，很合理地需要群組都具有一個名稱。</span><span class="sxs-lookup"><span data-stu-id="35984-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="35984-249">否則，連絡人組織成群組不是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="35984-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="35984-250">列表 6 包含新的測試表示這個意圖。</span><span class="sxs-lookup"><span data-stu-id="35984-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="35984-251">這項測試會驗證嘗試建立群組，而不需要提供名稱會導致模型狀態中的驗證錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="35984-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="35984-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

<span data-ttu-id="35984-253">為了滿足這項測試，我們必須將名稱屬性加入到群組類別 （請參閱列表 7）。</span><span class="sxs-lookup"><span data-stu-id="35984-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="35984-254">此外，我們需要將少許的驗證邏輯新增至群組控制器 s create （） 動作 （請參閱表 8）。</span><span class="sxs-lookup"><span data-stu-id="35984-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="35984-255">**Listing 7 - Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-255">**Listing 7 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

<span data-ttu-id="35984-256">**Listing 8 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-256">**Listing 8 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

<span data-ttu-id="35984-257">請注意群組控制器現在 create （） 動作包含驗證和資料庫的邏輯。</span><span class="sxs-lookup"><span data-stu-id="35984-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="35984-258">目前，群組控制站所使用的資料庫包含不超過記憶體中集合。</span><span class="sxs-lookup"><span data-stu-id="35984-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="35984-259">重構的時間</span><span class="sxs-lookup"><span data-stu-id="35984-259">Time to Refactor</span></span>

<span data-ttu-id="35984-260">第三個步驟，在 紅色/綠色/重構是重構部分。</span><span class="sxs-lookup"><span data-stu-id="35984-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="35984-261">到目前為止，我們要逐步從我們的程式碼，並考慮如何，我們可以重構我們的應用程式，以改善它的設計。</span><span class="sxs-lookup"><span data-stu-id="35984-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="35984-262">重構階段是在我們努力思考如何實作軟體設計原則和模式的最佳方式的階段。</span><span class="sxs-lookup"><span data-stu-id="35984-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="35984-263">我們可以自由修改我們的程式碼，以改善程式碼的設計，我們選擇的任何方式。</span><span class="sxs-lookup"><span data-stu-id="35984-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="35984-264">我們有防止我們小心破壞現有功能的單元測試的安全網。</span><span class="sxs-lookup"><span data-stu-id="35984-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="35984-265">現在，我們的群組控制站是從良好的軟體設計的觀點來看混亂。</span><span class="sxs-lookup"><span data-stu-id="35984-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="35984-266">群組控制站包含坎坷的混亂的驗證和資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="35984-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="35984-267">若要避免違反 Single Responsibility Principle，我們需要這些考量分成不同類別。</span><span class="sxs-lookup"><span data-stu-id="35984-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="35984-268">我們的重構的群組控制器類別包含在 列表 9。</span><span class="sxs-lookup"><span data-stu-id="35984-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="35984-269">控制器已修改成使用 ContactManager 服務層。</span><span class="sxs-lookup"><span data-stu-id="35984-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="35984-270">這是我們會使用與連絡人控制器的相同服務層。</span><span class="sxs-lookup"><span data-stu-id="35984-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="35984-271">列表 10 包含新方法新增至 ContactManager 服務層，以支援驗證、 列出及建立群組。</span><span class="sxs-lookup"><span data-stu-id="35984-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="35984-272">IContactManagerService 介面已更新為包含新的方法。</span><span class="sxs-lookup"><span data-stu-id="35984-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="35984-273">列表 11 會包含新的 FakeContactManagerRepository 類別可實作 IContactManagerRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="35984-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="35984-274">不同於也會實作 IContactManagerRepository 介面 EntityContactManagerRepository 類別，我們的新 FakeContactManagerRepository 類別不會不會與資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="35984-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="35984-275">FakeContactManagerRepository 類別會針對資料庫做為 proxy 中使用的記憶體中集合。</span><span class="sxs-lookup"><span data-stu-id="35984-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="35984-276">為假的儲存機制層，我們將在我們的單元測試中使用這個類別。</span><span class="sxs-lookup"><span data-stu-id="35984-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="35984-277">**Listing 9 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-277">**Listing 9 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

<span data-ttu-id="35984-278">**Listing 10 - Controllers\ContactManagerService.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-278">**Listing 10 - Controllers\ContactManagerService.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

<span data-ttu-id="35984-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]


<span data-ttu-id="35984-280">修改介面需要 IContactManagerRepository EntityContactManagerRepository 類別中實作的 CreateGroup() 和 ListGroups() 方法使用。</span><span class="sxs-lookup"><span data-stu-id="35984-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="35984-281">若要這樣做的 laziest 且最快速的方式是加入看起來像這樣的虛設常式方法：</span><span class="sxs-lookup"><span data-stu-id="35984-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]


<span data-ttu-id="35984-282">最後，這些變更，我們的應用程式的設計會要求我們對我們的單元測試進行一些修改。</span><span class="sxs-lookup"><span data-stu-id="35984-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="35984-283">我們現在需要執行單元測試時，使用 FakeContactManagerRepository。</span><span class="sxs-lookup"><span data-stu-id="35984-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="35984-284">列表 12 中，會包含更新的 GroupControllerTest 類別。</span><span class="sxs-lookup"><span data-stu-id="35984-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="35984-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

<span data-ttu-id="35984-286">我們進行所有這些之後，變更同樣地，所有我們的單元測試成功。</span><span class="sxs-lookup"><span data-stu-id="35984-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="35984-287">我們已完成紅色/綠色/重構整個的週期。</span><span class="sxs-lookup"><span data-stu-id="35984-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="35984-288">我們已實作的第一個的兩個使用者劇本。</span><span class="sxs-lookup"><span data-stu-id="35984-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="35984-289">我們現在有支援單元測試以使用者劇本的需求。</span><span class="sxs-lookup"><span data-stu-id="35984-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="35984-290">實作使用者劇本的其餘部分涉及重複相同的循環的紅色/綠色/重構。</span><span class="sxs-lookup"><span data-stu-id="35984-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="35984-291">修改資料庫</span><span class="sxs-lookup"><span data-stu-id="35984-291">Modifying our Database</span></span>

<span data-ttu-id="35984-292">不幸的是，即使我們已滿足所有需求表示我們的單元測試，我們的工作不是。</span><span class="sxs-lookup"><span data-stu-id="35984-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="35984-293">我們還是需要修改資料庫。</span><span class="sxs-lookup"><span data-stu-id="35984-293">We still need to modify our database.</span></span>

<span data-ttu-id="35984-294">我們需要建立新的群組資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-294">We need to create a new Group database table.</span></span> <span data-ttu-id="35984-295">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="35984-295">Follow these steps:</span></span>

1. <span data-ttu-id="35984-296">在 [伺服器總管] 視窗中，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取功能表選項**加入新的資料表**。</span><span class="sxs-lookup"><span data-stu-id="35984-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="35984-297">輸入 資料表設計工具，如下所述的兩個資料行。</span><span class="sxs-lookup"><span data-stu-id="35984-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="35984-298">識別碼資料行標示為主要金鑰和身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="35984-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="35984-299">按一下磁碟的圖示，名稱群組儲存新的資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.12_table01"></a>


| <span data-ttu-id="35984-300">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="35984-300">**Column Name**</span></span> | <span data-ttu-id="35984-301">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="35984-301">**Data Type**</span></span> | <span data-ttu-id="35984-302">**允許 null 值**</span><span class="sxs-lookup"><span data-stu-id="35984-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35984-303">ID</span><span class="sxs-lookup"><span data-stu-id="35984-303">Id</span></span> | <span data-ttu-id="35984-304">int</span><span class="sxs-lookup"><span data-stu-id="35984-304">int</span></span> | <span data-ttu-id="35984-305">False</span><span class="sxs-lookup"><span data-stu-id="35984-305">False</span></span> |
| <span data-ttu-id="35984-306">名稱</span><span class="sxs-lookup"><span data-stu-id="35984-306">Name</span></span> | <span data-ttu-id="35984-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="35984-307">nvarchar(50)</span></span> | <span data-ttu-id="35984-308">False</span><span class="sxs-lookup"><span data-stu-id="35984-308">False</span></span> |


<span data-ttu-id="35984-309">接下來，我們必須從 [連絡人] 資料表中刪除所有資料 （否則我們無法再建立的連絡人和群組的資料表之間的關聯性）。</span><span class="sxs-lookup"><span data-stu-id="35984-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won't be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="35984-310">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="35984-310">Follow these steps:</span></span>

1. <span data-ttu-id="35984-311">以滑鼠右鍵按一下 [連絡人] 資料表，然後選取功能表選項**顯示資料表資料**。</span><span class="sxs-lookup"><span data-stu-id="35984-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="35984-312">刪除所有資料列。</span><span class="sxs-lookup"><span data-stu-id="35984-312">Delete all of the rows.</span></span>

<span data-ttu-id="35984-313">接下來，我們需要定義群組的資料庫資料表和現有的連絡人資料庫資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="35984-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="35984-314">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="35984-314">Follow these steps:</span></span>

1. <span data-ttu-id="35984-315">按兩下以開啟 資料表設計工具的 伺服器總管 視窗中的 連絡人 資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="35984-316">將新的整數資料行加入至 Contacts 資料表名為 GroupId。</span><span class="sxs-lookup"><span data-stu-id="35984-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="35984-317">按一下 [關聯] 按鈕，以開啟外部索引鍵關聯性對話方塊 （見 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="35984-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="35984-318">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="35984-318">Click the Add button.</span></span>
5. <span data-ttu-id="35984-319">按一下 [顯示資料表和資料行規格] 按鈕旁邊的省略符號按鈕。</span><span class="sxs-lookup"><span data-stu-id="35984-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="35984-320">在 資料表和資料行 對話方塊中，選取 群組做為主要索引鍵資料行的識別碼與主索引鍵資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="35984-321">選取連絡人做為外部索引鍵資料表和外部索引鍵資料行的 GroupId （請參閱 圖 4）。</span><span class="sxs-lookup"><span data-stu-id="35984-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="35984-322">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="35984-322">Click the OK button.</span></span>
7. <span data-ttu-id="35984-323">底下**INSERT 及 UPDATE 規格**，選取值**Cascade** for**刪除規則**。</span><span class="sxs-lookup"><span data-stu-id="35984-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="35984-324">按一下 [關閉] 按鈕以關閉 [外部索引鍵關聯性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="35984-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="35984-325">按一下 [儲存] 按鈕，以將變更儲存至 Contacts 資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-325">Click the Save button to save the changes to the Contacts table.</span></span>


<span data-ttu-id="35984-326">[![建立資料庫資料表關聯性](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="35984-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span></span>

<span data-ttu-id="35984-327">**圖 03**:建立資料庫資料表關聯性 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="35984-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image6.png))</span></span>


<span data-ttu-id="35984-328">[![指定資料表關聯性](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="35984-328">[![Specifying table relationships](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span></span>

<span data-ttu-id="35984-329">**圖 04**:指定資料表關聯性 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="35984-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image8.png))</span></span>


### <a name="updating-our-data-model"></a><span data-ttu-id="35984-330">更新的資料模型</span><span class="sxs-lookup"><span data-stu-id="35984-330">Updating our Data Model</span></span>

<span data-ttu-id="35984-331">接下來，我們需要更新我們的資料模型，以代表新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="35984-332">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="35984-332">Follow these steps:</span></span>

1. <span data-ttu-id="35984-333">按兩下 ContactManagerModel.edmx 檔案以開啟 Entity Designer 的 模型 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="35984-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="35984-334">以滑鼠右鍵按一下設計工具介面，然後選取功能表選項**從資料庫更新模型**。</span><span class="sxs-lookup"><span data-stu-id="35984-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="35984-335">在 [更新精靈] 中，選取群組的資料表，然後按一下 [完成] 按鈕 （請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="35984-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="35984-336">以滑鼠右鍵按一下群組實體，然後選取功能表選項**重新命名**。</span><span class="sxs-lookup"><span data-stu-id="35984-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="35984-337">變更的名稱*群組*實體*群組*（個別）。</span><span class="sxs-lookup"><span data-stu-id="35984-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="35984-338">以滑鼠右鍵按一下連絡人實體下方會顯示群組導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="35984-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="35984-339">變更的名稱*群組*導覽屬性來*群組*（個別）。</span><span class="sxs-lookup"><span data-stu-id="35984-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>


<span data-ttu-id="35984-340">[![更新 Entity Framework 模型從資料庫](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="35984-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span></span>

<span data-ttu-id="35984-341">**圖 05**:更新 Entity Framework 模型從資料庫 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="35984-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image10.png))</span></span>


<span data-ttu-id="35984-342">完成這些步驟之後，您的資料模型會代表連絡人和群組的資料表。</span><span class="sxs-lookup"><span data-stu-id="35984-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="35984-343">實體設計工具應該會顯示這兩個實體 （請參閱 圖 6）。</span><span class="sxs-lookup"><span data-stu-id="35984-343">The Entity Designer should show both entities (see Figure 6).</span></span>


<span data-ttu-id="35984-344">[![顯示群組和連絡人的實體設計工具](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="35984-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span></span>

<span data-ttu-id="35984-345">**圖 06**:顯示群組和連絡人的實體設計工具 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="35984-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image12.png))</span></span>


### <a name="creating-our-repository-classes"></a><span data-ttu-id="35984-346">建立儲存機制類別</span><span class="sxs-lookup"><span data-stu-id="35984-346">Creating our Repository Classes</span></span>

<span data-ttu-id="35984-347">接下來，我們要實作儲存機制類別。</span><span class="sxs-lookup"><span data-stu-id="35984-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="35984-348">在這個反覆項目的過程中，我們加入數個新方法 IContactManagerRepository 介面撰寫程式碼，以符合我們的單元測試時。</span><span class="sxs-lookup"><span data-stu-id="35984-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="35984-349">IContactManagerRepository 介面的最終版本會包含在 列表 14。</span><span class="sxs-lookup"><span data-stu-id="35984-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="35984-350">**Listing 14 - Models\IContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-350">**Listing 14 - Models\IContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

<span data-ttu-id="35984-351">我們實際上尚未實作任何使用我們的實際 EntityContactManagerRepository 類別中的連絡人群組相關聯的方法。</span><span class="sxs-lookup"><span data-stu-id="35984-351">We haven't actually implemented any of the methods related to working with contact groups in our real EntityContactManagerRepository class.</span></span> <span data-ttu-id="35984-352">目前，EntityContactManagerRepository 類別具有虛設常式方法的每個 IContactManagerRepository 介面中所列的連絡人群組方法。</span><span class="sxs-lookup"><span data-stu-id="35984-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="35984-353">比方說，ListGroups() 方法目前看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="35984-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

<span data-ttu-id="35984-354">虛設常式方法可讓我們來編譯應用程式，並通過單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="35984-355">不過，現在就來實際實作這些方法。</span><span class="sxs-lookup"><span data-stu-id="35984-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="35984-356">EntityContactManagerRepository 類別的最終版本會包含在 列表 13。</span><span class="sxs-lookup"><span data-stu-id="35984-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="35984-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="35984-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a><span data-ttu-id="35984-358">建立檢視</span><span class="sxs-lookup"><span data-stu-id="35984-358">Creating the Views</span></span>

<span data-ttu-id="35984-359">當您使用預設 ASP.NET 檢視引擎 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="35984-360">因此，您不要建立檢視以回應特定的單元測試。</span><span class="sxs-lookup"><span data-stu-id="35984-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="35984-361">不過，因為應用程式會是不具有檢視毫無用處，我們可以 t 完成此反覆項目，而不需要建立和修改連絡人管理員應用程式中包含的檢視。</span><span class="sxs-lookup"><span data-stu-id="35984-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="35984-362">我們需要建立下列新檢視，可管理連絡人群組 （請參閱 圖 7）：</span><span class="sxs-lookup"><span data-stu-id="35984-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="35984-363">Views\Group\Index.aspx-連絡人群組的顯示清單</span><span class="sxs-lookup"><span data-stu-id="35984-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="35984-364">Views\Group\Delete.aspx-刪除連絡人群組會顯示確認表單</span><span class="sxs-lookup"><span data-stu-id="35984-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>


<span data-ttu-id="35984-365">[![群組索引檢視](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="35984-365">[![The Group Index view](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span></span>

<span data-ttu-id="35984-366">**圖 07**:群組 [索引] 檢視 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="35984-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image14.png))</span></span>


<span data-ttu-id="35984-367">我們需要修改下列現有的檢視，讓它們包含連絡人群組：</span><span class="sxs-lookup"><span data-stu-id="35984-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="35984-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="35984-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="35984-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="35984-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="35984-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="35984-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="35984-371">您可以看到修改過的檢視，查看隨附此教學課程的 Visual Studio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35984-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="35984-372">例如，圖 8 說明連絡人索引檢視。</span><span class="sxs-lookup"><span data-stu-id="35984-372">For example, Figure 8 illustrates the Contact Index view.</span></span>


<span data-ttu-id="35984-373">[![請連絡 [索引] 檢視](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="35984-373">[![The Contact Index view](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span></span>

<span data-ttu-id="35984-374">**圖 08**:請連絡 [索引] 檢視 ([按一下以檢視完整大小的影像](iteration-6-use-test-driven-development-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="35984-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image16.png))</span></span>


## <a name="summary"></a><span data-ttu-id="35984-375">總結</span><span class="sxs-lookup"><span data-stu-id="35984-375">Summary</span></span>

<span data-ttu-id="35984-376">在這個反覆項目，我們新增的新功能至我們的連絡人管理員應用程式依照測試導向開發的應用程式的設計方法。</span><span class="sxs-lookup"><span data-stu-id="35984-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="35984-377">我們已開始建立一組使用者劇本。</span><span class="sxs-lookup"><span data-stu-id="35984-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="35984-378">我們會建立一組單元測試，對應至使用者劇本所表示的需求。</span><span class="sxs-lookup"><span data-stu-id="35984-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="35984-379">最後，我們會撰寫剛好足夠的程式碼，以滿足需求的單元測試來表示。</span><span class="sxs-lookup"><span data-stu-id="35984-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="35984-380">我們已完成寫入足夠的程式碼，以滿足單元測試所表示的需求之後，我們會更新我們的資料庫和檢視表。</span><span class="sxs-lookup"><span data-stu-id="35984-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="35984-381">我們加入我們的資料庫中的新群組的資料表，並更新我們的 Entity Framework 資料模型。</span><span class="sxs-lookup"><span data-stu-id="35984-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="35984-382">我們也會建立並修改一組檢視。</span><span class="sxs-lookup"><span data-stu-id="35984-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="35984-383">在下一個反覆項目-最後一個反覆項目-我們重新撰寫我們的應用程式，才能利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="35984-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="35984-384">利用 Ajax，我們將會改善回應性和連絡人管理員應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="35984-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="35984-385">[上一頁](iteration-5-create-unit-tests-vb.md)
> [下一頁](iteration-7-add-ajax-functionality-vb.md)</span><span class="sxs-lookup"><span data-stu-id="35984-385">[Previous](iteration-5-create-unit-tests-vb.md)
[Next](iteration-7-add-ajax-functionality-vb.md)</span></span>
