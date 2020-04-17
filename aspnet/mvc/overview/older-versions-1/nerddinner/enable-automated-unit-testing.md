---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 開啟自動單元測試 |微軟文件
author: rick-anderson
description: 步驟 12 演示如何開發一套自動單元測試,以驗證我們的 NerdDinner 功能,這將讓我們有信心進行更改...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 7fe84efd9e4cc359c19d5ab9e22c579b80207e9c
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541464"
---
# <a name="enable-automated-unit-testing"></a><span data-ttu-id="f7b57-103">啟用自動化單元測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-103">Enable Automated Unit Testing</span></span>

<span data-ttu-id="f7b57-104">由[微軟](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f7b57-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f7b57-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f7b57-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f7b57-106">這是一個免費的[「NerdDinner」應用程式教程](introducing-the-nerddinner-tutorial.md)的第12步,它介紹了如何使用 ASP.NETmVC 1構建小型但完整的Web應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b57-106">This is step 12 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f7b57-107">步驟 12 演示如何開發一套自動單元測試,以驗證我們的 NerdDinner 功能,這將讓我們有信心在未來對應用程式進行更改和改進。</span><span class="sxs-lookup"><span data-stu-id="f7b57-107">Step 12 shows how to develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>
> 
> <span data-ttu-id="f7b57-108">如果您使用的是ASP.NET MVC 3,我們建議您按照[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音樂商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程進行操作。</span><span class="sxs-lookup"><span data-stu-id="f7b57-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-12-unit-testing"></a><span data-ttu-id="f7b57-109">神經晚餐步驟 12:單元測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-109">NerdDinner Step 12: Unit Testing</span></span>

<span data-ttu-id="f7b57-110">讓我們開發一套自動單元測試,以驗證我們的NerdDinner功能,這將讓我們有信心在未來對應用程式進行更改和改進。</span><span class="sxs-lookup"><span data-stu-id="f7b57-110">Let's develop a suite of automated unit tests that verify our NerdDinner functionality, and which will give us the confidence to make changes and improvements to the application in the future.</span></span>

### <a name="why-unit-test"></a><span data-ttu-id="f7b57-111">為什麼選擇單元測試?</span><span class="sxs-lookup"><span data-stu-id="f7b57-111">Why Unit Test?</span></span>

<span data-ttu-id="f7b57-112">在一天早上上班時,你突然閃現出一些關於你正在處理的應用程序的靈感。</span><span class="sxs-lookup"><span data-stu-id="f7b57-112">On the drive into work one morning you have a sudden flash of inspiration about an application you are working on.</span></span> <span data-ttu-id="f7b57-113">您意識到,您可以實現一個更改,這將使應用程式顯著更好地。</span><span class="sxs-lookup"><span data-stu-id="f7b57-113">You realize there is a change you can implement that will make the application dramatically better.</span></span> <span data-ttu-id="f7b57-114">它可能是清理代碼、添加新功能或修復 Bug 的重構。</span><span class="sxs-lookup"><span data-stu-id="f7b57-114">It might be a refactoring that cleans up the code, adds a new feature, or fixes a bug.</span></span>

<span data-ttu-id="f7b57-115">當你到達計算機時,您面臨的問題是「進行這種改進有多安全?</span><span class="sxs-lookup"><span data-stu-id="f7b57-115">The question that confronts you when you arrive at your computer is – "how safe is it to make this improvement?"</span></span> <span data-ttu-id="f7b57-116">如果做出改變有副作用或破壞某些東西呢?</span><span class="sxs-lookup"><span data-stu-id="f7b57-116">What if making the change has side effects or breaks something?</span></span> <span data-ttu-id="f7b57-117">更改可能很簡單,只需幾分鐘即可實現,但如果手動測試所有應用程式方案需要數小時,該怎麼辦?</span><span class="sxs-lookup"><span data-stu-id="f7b57-117">The change might be simple and only take a few minutes to implement, but what if it takes hours to manually test out all of the application scenarios?</span></span> <span data-ttu-id="f7b57-118">如果您忘記覆蓋場景,而損壞的應用程式投入生產,該怎麼辦?</span><span class="sxs-lookup"><span data-stu-id="f7b57-118">What if you forget to cover a scenario and a broken application goes into production?</span></span> <span data-ttu-id="f7b57-119">做出這種改進真的值得付出所有努力嗎?</span><span class="sxs-lookup"><span data-stu-id="f7b57-119">Is making this improvement really worth all the effort?</span></span>

<span data-ttu-id="f7b57-120">自動單元測試可以提供一個安全網,使您能夠持續增強應用程式,並避免害怕您正在處理的代碼。</span><span class="sxs-lookup"><span data-stu-id="f7b57-120">Automated unit tests can provide a safety net that enables you to continually enhance your applications, and avoid being afraid of the code you are working on.</span></span> <span data-ttu-id="f7b57-121">通過自動測試來快速驗證功能,使您能夠自信地編寫代碼,並使您能夠做出改進,否則您可能覺得這樣做並不自在。</span><span class="sxs-lookup"><span data-stu-id="f7b57-121">Having automated tests that quickly verify functionality enables you to code with confidence – and empower you to make improvements you might otherwise not have felt comfortable doing.</span></span> <span data-ttu-id="f7b57-122">它們還有助於創建更可維護且使用壽命更長的解決方案,從而獲得更高的投資回報。</span><span class="sxs-lookup"><span data-stu-id="f7b57-122">They also help create solutions that are more maintainable and have a longer lifetime - which leads to a much higher return on investment.</span></span>

<span data-ttu-id="f7b57-123">ASP.NET MVC 框架使單元測試應用程式功能變得簡單自然。</span><span class="sxs-lookup"><span data-stu-id="f7b57-123">The ASP.NET MVC Framework makes it easy and natural to unit test application functionality.</span></span> <span data-ttu-id="f7b57-124">它還支援測試驅動開發 (TDD) 工作流,支援基於測試優先的開發。</span><span class="sxs-lookup"><span data-stu-id="f7b57-124">It also enables a Test Driven Development (TDD) workflow that enables test-first based development.</span></span>

### <a name="nerddinnertests-project"></a><span data-ttu-id="f7b57-125">內德晚餐.測試專案</span><span class="sxs-lookup"><span data-stu-id="f7b57-125">NerdDinner.Tests Project</span></span>

<span data-ttu-id="f7b57-126">當我們在本教程開始時創建NerdDinner 應用程式時,系統會提示我們進行一個對話框,詢問我們是否希望創建一個單元測試專案以配合應用程式專案:</span><span class="sxs-lookup"><span data-stu-id="f7b57-126">When we created our NerdDinner application at the beginning of this tutorial, we were prompted with a dialog asking whether we wanted to create a unit test project to go along with the application project:</span></span>

![](enable-automated-unit-testing/_static/image1.png)

<span data-ttu-id="f7b57-127">我們保留了「是,創建一個單元測試專案」單選按鈕 -導致「NerdDinner.Test」專案被添加到我們的解決方案中:</span><span class="sxs-lookup"><span data-stu-id="f7b57-127">We kept the "Yes, create a unit test project" radio button selected – which resulted in a "NerdDinner.Tests" project being added to our solution:</span></span>

![](enable-automated-unit-testing/_static/image2.png)

<span data-ttu-id="f7b57-128">NerdDinner.測試專案引用NerdDinner應用程式專案程式集,並使我們能夠輕鬆地向其添加自動測試,以驗證應用程式功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-128">The NerdDinner.Tests project references the NerdDinner application project assembly, and enables us to easily add automated tests to it that verify the application functionality.</span></span>

### <a name="creating-unit-tests-for-our-dinner-model-class"></a><span data-ttu-id="f7b57-129">為我們的晚餐模型類創建單元測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-129">Creating Unit Tests for our Dinner Model Class</span></span>

<span data-ttu-id="f7b57-130">讓我們向NerdDinner.測試專案添加一些測試,以驗證我們在構建模型層時創建的Dinner類。</span><span class="sxs-lookup"><span data-stu-id="f7b57-130">Let's add some tests to our NerdDinner.Tests project that verify the Dinner class we created when we built our model layer.</span></span>

<span data-ttu-id="f7b57-131">我們將首先在我們的測試項目中創建一個名為"模型"的新資料夾,我們將在這裡放置與模型相關的測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-131">We'll start by creating a new folder within our test project called "Models" where we'll place our model-related tests.</span></span> <span data-ttu-id="f7b57-132">然後,我們將右鍵單擊該資料夾並選擇 **「添加&gt;- 新測試」** 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="f7b57-132">We'll then right-click on the folder and choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="f7b57-133">這將彈出「添加新測試」對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f7b57-133">This will bring up the "Add New Test" dialog.</span></span>

<span data-ttu-id="f7b57-134">我們將選擇創建「單元測試」並將其命名為「DinnerTest.cs」:</span><span class="sxs-lookup"><span data-stu-id="f7b57-134">We'll choose to create a "Unit Test" and name it "DinnerTest.cs":</span></span>

![](enable-automated-unit-testing/_static/image3.png)

<span data-ttu-id="f7b57-135">當我們按下「ok」按鈕 Visual Studio 會向專案添加(並打開)DinnerTest.cs 檔時:</span><span class="sxs-lookup"><span data-stu-id="f7b57-135">When we click the "ok" button Visual Studio will add (and open) a DinnerTest.cs file to the project:</span></span>

![](enable-automated-unit-testing/_static/image4.png)

<span data-ttu-id="f7b57-136">默認的 Visual Studio 單元測試範本內有一堆樣板代碼,我覺得有點亂。</span><span class="sxs-lookup"><span data-stu-id="f7b57-136">The default Visual Studio unit test template has a bunch of boiler-plate code within it that I find a little messy.</span></span> <span data-ttu-id="f7b57-137">讓我們清理它,以便只包含以下代碼:</span><span class="sxs-lookup"><span data-stu-id="f7b57-137">Let's clean it up to just contain the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

<span data-ttu-id="f7b57-138">上面的 DinnerTest 類上的 [TestClass] 屬性將其識別為包含測試的類以及可選的測試初始化和拆解代碼。</span><span class="sxs-lookup"><span data-stu-id="f7b57-138">The [TestClass] attribute on the DinnerTest class above identifies it as a class that will contain tests, as well as optional test initialization and teardown code.</span></span> <span data-ttu-id="f7b57-139">我們可以通過在其中添加具有 [TestMethod] 屬性的公共方法來定義其中的測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-139">We can define tests within it by adding public methods that have a [TestMethod] attribute on them.</span></span>

<span data-ttu-id="f7b57-140">下面是我們將添加的兩個測試中的第一個,即鍛煉我們的晚餐課程。</span><span class="sxs-lookup"><span data-stu-id="f7b57-140">Below are the first of two tests we'll add that exercise our Dinner class.</span></span> <span data-ttu-id="f7b57-141">第一個測試驗證,如果新晚餐的創建沒有正確設置所有屬性,則我們的晚餐無效。</span><span class="sxs-lookup"><span data-stu-id="f7b57-141">The first test verifies that our Dinner is invalid if a new Dinner is created without all properties being set correctly.</span></span> <span data-ttu-id="f7b57-142">第二個測試驗證我們的晚餐是否有效,當晚餐具有具有有效值的所有屬性設置時:</span><span class="sxs-lookup"><span data-stu-id="f7b57-142">The second test verifies that our Dinner is valid when a Dinner has all properties set with valid values:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

<span data-ttu-id="f7b57-143">您在上面會注意到我們的測試名稱非常明確(而且有些詳細)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-143">You'll notice above that our test names are very explicit (and somewhat verbose).</span></span> <span data-ttu-id="f7b57-144">我們這樣做是因為我們可能最終創建數百或數千個小測試,我們希望能夠輕鬆快速確定每個測試程序的意圖和行為(尤其是在查看測試運行程式中的失敗清單時)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-144">We are doing this because we might end up creating hundreds or thousands of small tests, and we want to make it easy to quickly determine the intent and behavior of each of them (especially when we are looking through a list of failures in a test runner).</span></span> <span data-ttu-id="f7b57-145">測試名稱應以測試的功能命名。</span><span class="sxs-lookup"><span data-stu-id="f7b57-145">The test names should be named after the functionality they are testing.</span></span> <span data-ttu-id="f7b57-146">上面我們使用的是"名詞\_\_應該動詞"命名模式。</span><span class="sxs-lookup"><span data-stu-id="f7b57-146">Above we are using a "Noun\_Should\_Verb" naming pattern.</span></span>

<span data-ttu-id="f7b57-147">我們使用「AAA」測試模式構建測試,該模式代表「安排、操作、斷言」:</span><span class="sxs-lookup"><span data-stu-id="f7b57-147">We are structuring the tests using the "AAA" testing pattern – which stands for "Arrange, Act, Assert":</span></span>

- <span data-ttu-id="f7b57-148">排列:設定正在測試的裝置</span><span class="sxs-lookup"><span data-stu-id="f7b57-148">Arrange: Setup the unit being tested</span></span>
- <span data-ttu-id="f7b57-149">操作:鍛煉被測試的單位並捕獲結果</span><span class="sxs-lookup"><span data-stu-id="f7b57-149">Act: Exercise the unit under test and capture results</span></span>
- <span data-ttu-id="f7b57-150">斷言:驗證行為</span><span class="sxs-lookup"><span data-stu-id="f7b57-150">Assert: Verify the behavior</span></span>

<span data-ttu-id="f7b57-151">當我們編寫測試時,我們希望避免讓單個測試執行太多操作。</span><span class="sxs-lookup"><span data-stu-id="f7b57-151">When we write tests we want to avoid having the individual tests do too much.</span></span> <span data-ttu-id="f7b57-152">相反,每個測試應只驗證一個概念(這將使確定故障原因變得更加容易)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-152">Instead each test should verify only a single concept (which will make it much easier to pinpoint the cause of failures).</span></span> <span data-ttu-id="f7b57-153">一個好的準則是嘗試每個測試只有一個斷言語句。</span><span class="sxs-lookup"><span data-stu-id="f7b57-153">A good guideline is to try and only have a single assert statement for each test.</span></span> <span data-ttu-id="f7b57-154">如果在測試方法中有多個斷言語句,請確保它們都用於測試同一概念。</span><span class="sxs-lookup"><span data-stu-id="f7b57-154">If you have more than one assert statement in a test method, make sure they are all being used to test the same concept.</span></span> <span data-ttu-id="f7b57-155">如有疑問,再做一次測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-155">When in doubt, make another test.</span></span>

### <a name="running-tests"></a><span data-ttu-id="f7b57-156">正在執行測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-156">Running Tests</span></span>

<span data-ttu-id="f7b57-157">Visual Studio 2008 專業版(和更高版本)包括一個內置測試運行程式,可用於在 IDE 中運行 Visual Studio 單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="f7b57-157">Visual Studio 2008 Professional (and higher editions) includes a built-in test runner that can be used to run Visual Studio Unit Test projects within the IDE.</span></span> <span data-ttu-id="f7b57-158">我們可以選擇解決方案選單**中的&gt;「&gt;測試- 執行-所有測試**」命令(或鍵入 Ctrl R,A)來執行我們所有的單元測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-158">We can select the **Test-&gt;Run-&gt;All Tests in Solution** menu command (or type Ctrl R, A) to run all of our unit tests.</span></span> <span data-ttu-id="f7b57-159">或者,我們可以將游標定位到特定的測試類或測試方法中,並使用**當前上下文菜單&gt;中的&gt;測試運行 測試**命令(或鍵入 Ctrl R、T)來運行單元測試的子集。</span><span class="sxs-lookup"><span data-stu-id="f7b57-159">Or alternatively we can position our cursor within a specific test class or test method and use the **Test-&gt;Run-&gt;Tests in Current Context** menu command (or type Ctrl R, T) to run a subset of the unit tests.</span></span>

<span data-ttu-id="f7b57-160">讓我們將游標定位在 DinnerTest 類中,並鍵入"Ctrl R,T"以運行我們剛剛定義的兩個測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-160">Let's position our cursor within the DinnerTest class and type "Ctrl R, T" to run the two tests we just defined.</span></span> <span data-ttu-id="f7b57-161">當我們執行此操作時,Visual Studio 中將顯示一個「測試結果」視窗,我們將看到其中列出的測試運行結果:</span><span class="sxs-lookup"><span data-stu-id="f7b57-161">When we do this a "Test Results" window will appear within Visual Studio and we'll see the results of our test run listed within it:</span></span>

![](enable-automated-unit-testing/_static/image5.png)

<span data-ttu-id="f7b57-162">*注意:預設情況下,VS 測試結果視窗不顯示"類名稱"列。您可以通過在「測試結果」視窗中右鍵按下並使用「添加/刪除列」選單命令來添加此內容。*</span><span class="sxs-lookup"><span data-stu-id="f7b57-162">*Note: The VS test results window does not show the Class Name column by default. You can add this by right-clicking within the Test Results window and using the Add/Remove Columns menu command.*</span></span>

<span data-ttu-id="f7b57-163">我們的兩個測試只用了一小部分時間就可以運行了,正如您所看到的,它們都通過了。</span><span class="sxs-lookup"><span data-stu-id="f7b57-163">Our two tests took only a fraction of a second to run – and as you can see they both passed.</span></span> <span data-ttu-id="f7b57-164">現在,我們可以通過創建驗證特定規則驗證的其他測試來擴展它們,並涵蓋我們添加到 Dinner 類的兩種説明方法 - IsUserHost() 和 IsUser 註冊()。</span><span class="sxs-lookup"><span data-stu-id="f7b57-164">We can now go on and augment them by creating additional tests that verify specific rule validations, as well as cover the two helper methods - IsUserHost() and IsUserRegistered() – that we added to the Dinner class.</span></span> <span data-ttu-id="f7b57-165">為 Dinner 類提供所有這些測試將使將來向該課程添加新業務規則和驗證變得更加簡單和安全。</span><span class="sxs-lookup"><span data-stu-id="f7b57-165">Having all these tests in place for the Dinner class will make it much easier and safer to add new business rules and validations to it in the future.</span></span> <span data-ttu-id="f7b57-166">我們可以將新的規則邏輯添加到 Dinner,然後在幾秒鐘內驗證它是否沒有破壞我們以前的任何邏輯功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-166">We can add our new rule logic to Dinner, and then within seconds verify that it hasn't broken any of our previous logic functionality.</span></span>

<span data-ttu-id="f7b57-167">請注意,使用描述性測試名稱如何便於快速瞭解每個測試正在驗證的內容。</span><span class="sxs-lookup"><span data-stu-id="f7b57-167">Notice how using a descriptive test name makes it easy to quickly understand what each test is verifying.</span></span> <span data-ttu-id="f7b57-168">我建議使用 **「工具&gt;- 選項」** 選單命令,打開&gt;測試工具- 測試執行設定螢幕,並選取中「按兩下失敗或不確定的單位測試結果顯示測試中的失敗點」複選框。</span><span class="sxs-lookup"><span data-stu-id="f7b57-168">I recommend using the **Tools-&gt;Options** menu command, opening the Test Tools-&gt;Test Execution configuration screen, and checking the "Double-clicking a failed or inconclusive unit test result displays the point of failure in the test" checkbox.</span></span> <span data-ttu-id="f7b57-169">這將允許您雙擊測試結果視窗中的故障,並立即跳轉到斷言失敗。</span><span class="sxs-lookup"><span data-stu-id="f7b57-169">This will allow you to double-click on a failure in the test results window and jump immediately to the assert failure.</span></span>

### <a name="creating-dinnerscontroller-unit-tests"></a><span data-ttu-id="f7b57-170">建立晚餐控制器單元測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-170">Creating DinnersController Unit Tests</span></span>

<span data-ttu-id="f7b57-171">現在,讓我們創建一些單元測試,以驗證我們的 DinnersController 功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-171">Let's now create some unit tests that verify our DinnersController functionality.</span></span> <span data-ttu-id="f7b57-172">我們將從右鍵單擊測試專案中的"控制器"資料夾開始,然後選擇**&gt;「新增測試」** 功能表命令。</span><span class="sxs-lookup"><span data-stu-id="f7b57-172">We'll start by right-clicking on the "Controllers" folder within our Test project and then choose the **Add-&gt;New Test** menu command.</span></span> <span data-ttu-id="f7b57-173">我們將創建一個「單元測試」並將其命名為「DinnersControllerTest.cs」。</span><span class="sxs-lookup"><span data-stu-id="f7b57-173">We'll create a "Unit Test" and name it "DinnersControllerTest.cs".</span></span>

<span data-ttu-id="f7b57-174">我們將創建兩種測試方法,以驗證 DinnersController 上的細節() 操作方法。</span><span class="sxs-lookup"><span data-stu-id="f7b57-174">We'll create two test methods that verify the Details() action method on the DinnersController.</span></span> <span data-ttu-id="f7b57-175">第一個將驗證在請求現有晚餐時是否返回了視圖。</span><span class="sxs-lookup"><span data-stu-id="f7b57-175">The first will verify that a View is returned when an existing Dinner is requested.</span></span> <span data-ttu-id="f7b57-176">第二個將驗證在請求不存在的晚餐時是否返回「未找到」檢視:</span><span class="sxs-lookup"><span data-stu-id="f7b57-176">The second will verify that a "NotFound" view is returned when a non-existent Dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

<span data-ttu-id="f7b57-177">上述代碼編譯乾淨。</span><span class="sxs-lookup"><span data-stu-id="f7b57-177">The above code compiles clean.</span></span> <span data-ttu-id="f7b57-178">但是,當我們運行測試時,它們都失敗:</span><span class="sxs-lookup"><span data-stu-id="f7b57-178">When we run the tests, though, they both fail:</span></span>

![](enable-automated-unit-testing/_static/image6.png)

<span data-ttu-id="f7b57-179">如果我們查看錯誤消息,我們將看到測試失敗的原因是因為我們的 DinnersRepository 類無法連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7b57-179">If we look at the error messages, we'll see that the reason the tests failed was because our DinnersRepository class was unable to connect to a database.</span></span> <span data-ttu-id="f7b57-180">我們的NerdDinner應用程式使用連接字串到本地SQL Server Express檔案,該檔\_位於NerdDinner應用程式專案的#App資料目錄下。</span><span class="sxs-lookup"><span data-stu-id="f7b57-180">Our NerdDinner application is using a connection-string to a local SQL Server Express file which lives under the \App\_Data directory of the NerdDinner application project.</span></span> <span data-ttu-id="f7b57-181">由於我們的NerdDinner.測試專案編譯並運行在不同的目錄中,然後以應用程式專案運行,因此連接字串的相對路徑位置不正確。</span><span class="sxs-lookup"><span data-stu-id="f7b57-181">Because our NerdDinner.Tests project compiles and runs in a different directory then the application project, the relative path location of our connection-string is incorrect.</span></span>

<span data-ttu-id="f7b57-182">*我們可以*通過將 SQL Express 資料庫檔案複製到測試專案來解決此問題,然後在測試專案的 App.config 中向它添加適當的測試連接字串。</span><span class="sxs-lookup"><span data-stu-id="f7b57-182">We *could* fix this by copying the SQL Express database file to our test project, and then add an appropriate test connection-string to it in the App.config of our test project.</span></span> <span data-ttu-id="f7b57-183">這將使上述測試解除阻止並運行。</span><span class="sxs-lookup"><span data-stu-id="f7b57-183">This would get the above tests unblocked and running.</span></span>

<span data-ttu-id="f7b57-184">但是,使用真實資料庫的單位測試代碼帶來了許多挑戰。</span><span class="sxs-lookup"><span data-stu-id="f7b57-184">Unit testing code using a real database, though, brings with it a number of challenges.</span></span> <span data-ttu-id="f7b57-185">具體來說：</span><span class="sxs-lookup"><span data-stu-id="f7b57-185">Specifically:</span></span>

- <span data-ttu-id="f7b57-186">它顯著減慢了單元測試的執行時間。</span><span class="sxs-lookup"><span data-stu-id="f7b57-186">It significantly slows down the execution time of unit tests.</span></span> <span data-ttu-id="f7b57-187">運行測試所需的時間越長,執行測試的可能性就越小。</span><span class="sxs-lookup"><span data-stu-id="f7b57-187">The longer it takes to run tests, the less likely you are to execute them frequently.</span></span> <span data-ttu-id="f7b57-188">理想情況下,您希望單元測試能夠在幾秒鐘內運行,並且讓它像編譯項目一樣自然地完成。</span><span class="sxs-lookup"><span data-stu-id="f7b57-188">Ideally you want your unit tests to be able to be run in seconds – and have it be something you do as naturally as compiling the project.</span></span>
- <span data-ttu-id="f7b57-189">它在測試中使設置和清理邏輯複雜化。</span><span class="sxs-lookup"><span data-stu-id="f7b57-189">It complicates the setup and cleanup logic within tests.</span></span> <span data-ttu-id="f7b57-190">您希望每個單元測試都隔離並獨立於其他測試(沒有副作用或依賴項)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-190">You want each unit test to be isolated and independent of others (with no side effects or dependencies).</span></span> <span data-ttu-id="f7b57-191">在對真實資料庫工作時,您必須注意狀態並在測試之間重置它。</span><span class="sxs-lookup"><span data-stu-id="f7b57-191">When working against a real database you have to be mindful of state and reset it between tests.</span></span>

<span data-ttu-id="f7b57-192">讓我們來看看一種稱為"依賴注入"的設計模式,它可以幫助我們解決這些問題,並避免使用真實資料庫作為測試的需要。</span><span class="sxs-lookup"><span data-stu-id="f7b57-192">Let's look at a design pattern called "dependency injection" that can help us work around these issues and avoid the need to use a real database with our tests.</span></span>

### <a name="dependency-injection"></a><span data-ttu-id="f7b57-193">相依性插入</span><span class="sxs-lookup"><span data-stu-id="f7b57-193">Dependency Injection</span></span>

<span data-ttu-id="f7b57-194">現在,晚餐控制器與晚餐存儲庫類緊密地"耦合"。</span><span class="sxs-lookup"><span data-stu-id="f7b57-194">Right now DinnersController is tightly "coupled" to the DinnerRepository class.</span></span> <span data-ttu-id="f7b57-195">"耦合"是指類顯式依賴於另一個類才能工作的情況:</span><span class="sxs-lookup"><span data-stu-id="f7b57-195">"Coupling" refers to a situation where a class explicitly relies on another class in order to work:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

<span data-ttu-id="f7b57-196">由於 DinnerRepository 類需要訪問資料庫,因此 DinnersController 類在 DinnerRepository 上的緊密耦合依賴關係最終要求我們有一個資料庫才能測試 DinnersController 操作方法。</span><span class="sxs-lookup"><span data-stu-id="f7b57-196">Because the DinnerRepository class requires access to a database, the tightly coupled dependency the DinnersController class has on the DinnerRepository ends up requiring us to have a database in order for the DinnersController action methods to be tested.</span></span>

<span data-ttu-id="f7b57-197">我們可以採用稱為"依賴注入"的設計模式來克服這一問題,這種方法在使用依賴項(如提供數據訪問的存儲庫類)中不再隱式創建。</span><span class="sxs-lookup"><span data-stu-id="f7b57-197">We can get around this by employing a design pattern called "dependency injection" – which is an approach where dependencies (like repository classes that provide data access) are no longer implicitly created within classes that use them.</span></span> <span data-ttu-id="f7b57-198">相反,依賴項可以顯式傳遞給使用構造函數參數使用它們的類。</span><span class="sxs-lookup"><span data-stu-id="f7b57-198">Instead, dependencies can be explicitly passed to the class that uses them using constructor arguments.</span></span> <span data-ttu-id="f7b57-199">如果使用介面定義依賴項,則我們可以靈活地通過單元測試方案的"假"依賴項實現。</span><span class="sxs-lookup"><span data-stu-id="f7b57-199">If the dependencies are defined using interfaces, we then have the flexibility to pass in "fake" dependency implementations for unit test scenarios.</span></span> <span data-ttu-id="f7b57-200">這使我們能夠創建實際上不需要訪問資料庫的特定於測試的依賴項實現。</span><span class="sxs-lookup"><span data-stu-id="f7b57-200">This enables us to create test-specific dependency implementations that do not actually require access to a database.</span></span>

<span data-ttu-id="f7b57-201">為了看到此操作,讓我們使用 DinnersController 實現依賴項注入。</span><span class="sxs-lookup"><span data-stu-id="f7b57-201">To see this in action, let's implement dependency injection with our DinnersController.</span></span>

#### <a name="extracting-an-idinnerrepository-interface"></a><span data-ttu-id="f7b57-202">擷取 IDinner 儲存庫介面</span><span class="sxs-lookup"><span data-stu-id="f7b57-202">Extracting an IDinnerRepository interface</span></span>

<span data-ttu-id="f7b57-203">我們的第一步是創建一個新的 IDinnerRepository 介面,該介面封裝了控制器檢索和更新 Dinner 所需的儲存庫合同。</span><span class="sxs-lookup"><span data-stu-id="f7b57-203">Our first step will be to create a new IDinnerRepository interface that encapsulates the repository contract our controllers require to retrieve and update Dinners.</span></span>

<span data-ttu-id="f7b57-204">我們可以手動定義此介面協定,通過右鍵單擊 #Model 資料夾,然後選擇 **「添加-&gt;新專案」** 功能表命令並創建名為 IDinnerRepository.cs 的新介面。</span><span class="sxs-lookup"><span data-stu-id="f7b57-204">We can define this interface contract manually by right-clicking on the \Models folder, and then choosing the **Add-&gt;New Item** menu command and creating a new interface named IDinnerRepository.cs.</span></span>

<span data-ttu-id="f7b57-205">或者,我們可以使用內置於 Visual Studio 專業版(和更高版本)的重構工具,從現有的 DinnerRepository 類中自動提取和創建我們的介面。</span><span class="sxs-lookup"><span data-stu-id="f7b57-205">Alternatively we can use the refactoring tools built-into Visual Studio Professional (and higher editions) to automatically extract and create an interface for us from our existing DinnerRepository class.</span></span> <span data-ttu-id="f7b57-206">要使用 VS 擷取此介面,只需將游標放在 DinnerRepository 類別的文字編輯器中,然後右鍵按下選擇 **「重構-&gt;抽取介面」** 選單指令:</span><span class="sxs-lookup"><span data-stu-id="f7b57-206">To extract this interface using VS, simply position the cursor in the text editor on the DinnerRepository class, and then right-click and choose the **Refactor-&gt;Extract Interface** menu command:</span></span>

![](enable-automated-unit-testing/_static/image7.png)

<span data-ttu-id="f7b57-207">這將啟動「提取介面」對話框,並提示我們建立介面的名稱。</span><span class="sxs-lookup"><span data-stu-id="f7b57-207">This will launch the "Extract Interface" dialog and prompt us for the name of the interface to create.</span></span> <span data-ttu-id="f7b57-208">它將預設為 IDinnerRepository,並自動選擇現有 DinnerRepository 類上的所有公共方法以添加到介面:</span><span class="sxs-lookup"><span data-stu-id="f7b57-208">It will default to IDinnerRepository and automatically select all public methods on the existing DinnerRepository class to add to the interface:</span></span>

![](enable-automated-unit-testing/_static/image8.png)

<span data-ttu-id="f7b57-209">當我們按下「確定」按鈕時,Visual Studio 將為我們的應用程式添加新的 IDinnerRepository 介面:</span><span class="sxs-lookup"><span data-stu-id="f7b57-209">When we click the "ok" button, Visual Studio will add a new IDinnerRepository interface to our application:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

<span data-ttu-id="f7b57-210">我們現有的 DinnerRepository 類將被更新,以便實現介面:</span><span class="sxs-lookup"><span data-stu-id="f7b57-210">And our existing DinnerRepository class will be updated so that it implements the interface:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a><span data-ttu-id="f7b57-211">更新晚餐控制器以支援建構函數注入</span><span class="sxs-lookup"><span data-stu-id="f7b57-211">Updating DinnersController to support constructor injection</span></span>

<span data-ttu-id="f7b57-212">現在,我們將更新 DinnersController 類以使用新介面。</span><span class="sxs-lookup"><span data-stu-id="f7b57-212">We'll now update the DinnersController class to use the new interface.</span></span>

<span data-ttu-id="f7b57-213">目前,晚餐控制器是硬編碼的,因此其「晚餐存儲庫」欄位始終是一個晚餐存儲庫類:</span><span class="sxs-lookup"><span data-stu-id="f7b57-213">Currently DinnersController is hard-coded such that its "dinnerRepository" field is always a DinnerRepository class:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

<span data-ttu-id="f7b57-214">我們將更改它,以便「晚餐存儲庫」欄位是IDinner儲存庫類型,而不是晚餐儲存庫。</span><span class="sxs-lookup"><span data-stu-id="f7b57-214">We'll change it so that the "dinnerRepository" field is of type IDinnerRepository instead of DinnerRepository.</span></span> <span data-ttu-id="f7b57-215">然後,我們將添加兩個公共 DinnersController 構造函數。</span><span class="sxs-lookup"><span data-stu-id="f7b57-215">We'll then add two public DinnersController constructors.</span></span> <span data-ttu-id="f7b57-216">其中一個構造函數允許將IDinnerRepository作為參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="f7b57-216">One of the constructors allows an IDinnerRepository to be passed as an argument.</span></span> <span data-ttu-id="f7b57-217">另一個是使用我們現有的 DinnerRepository 實現的預設建構函數:</span><span class="sxs-lookup"><span data-stu-id="f7b57-217">The other is a default constructor that uses our existing DinnerRepository implementation:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

<span data-ttu-id="f7b57-218">由於預設情況下ASP.NET MVC 使用預設構造函數創建控制器類,因此運行時的 DinnersController 將繼續使用 DinnerRepository 類來執行數據訪問。</span><span class="sxs-lookup"><span data-stu-id="f7b57-218">Because ASP.NET MVC by default creates controller classes using default constructors, our DinnersController at runtime will continue to use the DinnerRepository class to perform data access.</span></span>

<span data-ttu-id="f7b57-219">但是,我們現在可以更新我們的單元測試,以便使用參數構造函數在"假"晚餐存儲庫實現中傳遞。</span><span class="sxs-lookup"><span data-stu-id="f7b57-219">We can now update our unit tests, though, to pass in a "fake" dinner repository implementation using the parameter constructor.</span></span> <span data-ttu-id="f7b57-220">此「假」晚餐存儲庫不需要訪問真實資料庫,而是使用記憶體中的範例數據。</span><span class="sxs-lookup"><span data-stu-id="f7b57-220">This "fake" dinner repository will not require access to a real database, and instead will use in-memory sample data.</span></span>

#### <a name="creating-the-fakedinnerrepository-class"></a><span data-ttu-id="f7b57-221">建立假晚餐儲存庫類</span><span class="sxs-lookup"><span data-stu-id="f7b57-221">Creating the FakeDinnerRepository class</span></span>

<span data-ttu-id="f7b57-222">讓我們創建一個假晚餐存儲庫類。</span><span class="sxs-lookup"><span data-stu-id="f7b57-222">Let's create a FakeDinnerRepository class.</span></span>

<span data-ttu-id="f7b57-223">我們將首先在我們的NerdDinner.測試項目中創建一個"Fakes"目錄,然後向它添加新的FakeDinnerRepository類(右鍵單擊該文件夾並選擇 **"&gt;添加- 新類**"):</span><span class="sxs-lookup"><span data-stu-id="f7b57-223">We'll begin by creating a "Fakes" directory within our NerdDinner.Tests project and then add a new FakeDinnerRepository class to it (right-click on the folder and choose **Add-&gt;New Class**):</span></span>

![](enable-automated-unit-testing/_static/image9.png)

<span data-ttu-id="f7b57-224">我們將更新代碼,以便 FakeDinnerRepository 類實現 IDinnerRepository 介面。</span><span class="sxs-lookup"><span data-stu-id="f7b57-224">We'll update the code so that the FakeDinnerRepository class implements the IDinnerRepository interface.</span></span> <span data-ttu-id="f7b57-225">然後,我們可以右鍵單擊它並選擇「實現介面 IDinnerRepository」上下文菜單命令:</span><span class="sxs-lookup"><span data-stu-id="f7b57-225">We can then right-click on it and choose the "Implement interface IDinnerRepository" context menu command:</span></span>

![](enable-automated-unit-testing/_static/image10.png)

<span data-ttu-id="f7b57-226">這將導致 Visual Studio 自動將所有 IDinnerRepository 介面成員添加到我們的 FakeDinnerRepository 類,並包含預設的「存分之外」實現:</span><span class="sxs-lookup"><span data-stu-id="f7b57-226">This will cause Visual Studio to automatically add all of the IDinnerRepository interface members to our FakeDinnerRepository class with default "stub out" implementations:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

<span data-ttu-id="f7b57-227">然後,我們可以更新 FakeDinnerRepository 實現,以處理作為構造函數參數&lt;傳遞&gt;給 它的 記憶體中清單晚餐集合:</span><span class="sxs-lookup"><span data-stu-id="f7b57-227">We can then update the FakeDinnerRepository implementation to work off of an in-memory List&lt;Dinner&gt; collection passed to it as a constructor argument:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

<span data-ttu-id="f7b57-228">我們現在有一個假的IDinnerRepository實現,它不需要資料庫,而是可以處理存儲中晚餐物件清單。</span><span class="sxs-lookup"><span data-stu-id="f7b57-228">We now have a fake IDinnerRepository implementation that does not require a database, and can instead work off an in-memory list of Dinner objects.</span></span>

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a><span data-ttu-id="f7b57-229">將假晚餐儲存庫與單元測試一起使用</span><span class="sxs-lookup"><span data-stu-id="f7b57-229">Using the FakeDinnerRepository with Unit Tests</span></span>

<span data-ttu-id="f7b57-230">讓我們返回到由於資料庫不可用而較早失敗的 DinnersController 單元測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-230">Let's return to the DinnersController unit tests that failed earlier because the database wasn't available.</span></span> <span data-ttu-id="f7b57-231">我們可以更新測試方法,使用以下代碼將填充在記憶體中晚餐數據樣本的假晚餐存儲庫更新給 DinnersController:</span><span class="sxs-lookup"><span data-stu-id="f7b57-231">We can update the test methods to use a FakeDinnerRepository populated with sample in-memory Dinner data to the DinnersController using the code below:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

<span data-ttu-id="f7b57-232">現在,當我們運行這些測試時,它們都通過了:</span><span class="sxs-lookup"><span data-stu-id="f7b57-232">And now when we run these tests they both pass:</span></span>

![](enable-automated-unit-testing/_static/image11.png)

<span data-ttu-id="f7b57-233">最重要的是,它們只需一小部分秒才能運行,並且不需要任何複雜的設置/清理邏輯。</span><span class="sxs-lookup"><span data-stu-id="f7b57-233">Best of all, they take only a fraction of a second to run, and do not require any complicated setup/cleanup logic.</span></span> <span data-ttu-id="f7b57-234">我們現在可以單元測試所有我們的 DinnersController 操作方法代碼(包括清單、分頁、詳細資訊、創建、更新和刪除),而無需連接到真正的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f7b57-234">We can now unit test all of our DinnersController action method code (including listing, paging, details, create, update and delete) without ever needing to connect to a real database.</span></span>

| <span data-ttu-id="f7b57-235">**側主題:相依項注入框架**</span><span class="sxs-lookup"><span data-stu-id="f7b57-235">**Side Topic: Dependency Injection Frameworks**</span></span> |
| --- |
| <span data-ttu-id="f7b57-236">執行手動依賴項注入(如上所示)工作正常,但隨著應用程式中依賴項和元件數量的增加,維護起來確實變得更加困難。</span><span class="sxs-lookup"><span data-stu-id="f7b57-236">Performing manual dependency injection (like we are above) works fine, but does become harder to maintain as the number of dependencies and components in an application increases.</span></span> <span data-ttu-id="f7b57-237">.NET 存在多個依賴項注入框架,可説明提供更多依賴項管理靈活性。</span><span class="sxs-lookup"><span data-stu-id="f7b57-237">Several dependency injection frameworks exist for .NET that can help provide even more dependency management flexibility.</span></span> <span data-ttu-id="f7b57-238">這些框架有時也稱為"控制反轉"(IoC) 容器,它們提供了機制,支援在運行時指定依賴項並將其傳遞給物件(通常使用構造函數注入)的額外配置支援級別。</span><span class="sxs-lookup"><span data-stu-id="f7b57-238">These frameworks, also sometimes called "Inversion of Control" (IoC) containers, provide mechanisms that enable an additional level of configuration support for specifying and passing dependencies to objects at runtime (most often using constructor injection).</span></span> <span data-ttu-id="f7b57-239">.NET 中一些較流行的 OSS 依賴項注入 / IOC 框架包括:AutoFac、Ninject、Spring.NET、結構映射和溫莎。</span><span class="sxs-lookup"><span data-stu-id="f7b57-239">Some of the more popular OSS Dependency Injection / IOC frameworks in .NET include: AutoFac, Ninject, Spring.NET, StructureMap, and Windsor.</span></span> <span data-ttu-id="f7b57-240">ASP.NET MVC 公開擴展 API,使開發人員能夠參與控制器的解析和實例化,並使依賴項注入/IoC 框架能夠安全地整合到此過程中。</span><span class="sxs-lookup"><span data-stu-id="f7b57-240">ASP.NET MVC exposes extensibility APIs that enable developers to participate in the resolution and instantiation of controllers, and which enables Dependency Injection / IoC frameworks to be cleanly integrated within this process.</span></span> <span data-ttu-id="f7b57-241">使用 DI/IOC 框架還將使我們能夠從 DinnersController 中刪除預設構造函數 , 這將完全消除它和 DinnerRepository 之間的耦合。</span><span class="sxs-lookup"><span data-stu-id="f7b57-241">Using a DI/IOC framework would also enable us to remove the default constructor from our DinnersController – which would completely remove the coupling between it and the DinnerRepository.</span></span> <span data-ttu-id="f7b57-242">我們不會使用依賴注入/IOC框架與我們的NerdDinner應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b57-242">We won't be using a dependency injection / IOC framework with our NerdDinner application.</span></span> <span data-ttu-id="f7b57-243">但是,如果NerdDinner代碼庫和功能的增長,我們可以考慮未來的問題。</span><span class="sxs-lookup"><span data-stu-id="f7b57-243">But it is something we could consider for the future if the NerdDinner code-base and capabilities grew.</span></span> |

### <a name="creating-edit-action-unit-tests"></a><span data-ttu-id="f7b57-244">建立編輯操作儲存單元測試</span><span class="sxs-lookup"><span data-stu-id="f7b57-244">Creating Edit Action Unit Tests</span></span>

<span data-ttu-id="f7b57-245">現在,讓我們創建一些單元測試,以驗證 DinnersController 的編輯功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-245">Let's now create some unit tests that verify the Edit functionality of the DinnersController.</span></span> <span data-ttu-id="f7b57-246">我們將首先測試我們的編輯操作的 HTTP-GET 版本:</span><span class="sxs-lookup"><span data-stu-id="f7b57-246">We'll start by testing the HTTP-GET version of our Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

<span data-ttu-id="f7b57-247">我們將創建一個測試,以驗證在請求有效晚餐時,由 DinnerFormViewModel 物件支援的視圖是否呈現回:</span><span class="sxs-lookup"><span data-stu-id="f7b57-247">We'll create a test that verifies that a View backed by a DinnerFormViewModel object is rendered back when a valid dinner is requested:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

<span data-ttu-id="f7b57-248">但是,當我們運行測試時,我們會發現它失敗,因為當 Edit 方法訪問User.Identity.Name屬性以執行 Dinner.Is託管By() 檢查時,將引發一個空引用異常。</span><span class="sxs-lookup"><span data-stu-id="f7b57-248">When we run the test, though, we'll find that it fails because a null reference exception is thrown when the Edit method accesses the User.Identity.Name property to perform the Dinner.IsHostedBy() check.</span></span>

<span data-ttu-id="f7b57-249">控制器基類上的 User 物件封裝有關登錄使用者的詳細資訊,並在執行時創建控制器時由 ASP.NET MVC 填充。</span><span class="sxs-lookup"><span data-stu-id="f7b57-249">The User object on the Controller base class encapsulates details about the logged-in user, and is populated by ASP.NET MVC when it creates the controller at runtime.</span></span> <span data-ttu-id="f7b57-250">由於我們在 Web 伺服器環境之外測試 DinnersController,所以未設置使用者物件(因此為空引用異常)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-250">Because we are testing the DinnersController outside of a web-server environment, the User object isn't set (hence the null reference exception).</span></span>

### <a name="mocking-the-useridentityname-property"></a><span data-ttu-id="f7b57-251">類比User.Identity.Name屬性</span><span class="sxs-lookup"><span data-stu-id="f7b57-251">Mocking the User.Identity.Name property</span></span>

<span data-ttu-id="f7b57-252">類比框架使我們能夠動態創建支援測試的從屬物件的假版本,從而使測試更容易。</span><span class="sxs-lookup"><span data-stu-id="f7b57-252">Mocking frameworks make testing easier by enabling us to dynamically create fake versions of dependent objects that support our tests.</span></span> <span data-ttu-id="f7b57-253">例如,我們可以在"編輯"操作測試中使用類比框架動態創建一個使用者物件,我們的 DinnersController 可用於查找模擬使用者名。</span><span class="sxs-lookup"><span data-stu-id="f7b57-253">For example, we can use a mocking framework in our Edit action test to dynamically create a User object that our DinnersController can use to lookup a simulated username.</span></span> <span data-ttu-id="f7b57-254">這將避免在運行測試時引發空引用。</span><span class="sxs-lookup"><span data-stu-id="f7b57-254">This will avoid a null reference from being thrown when we run our test.</span></span>

<span data-ttu-id="f7b57-255">有許多 .NET 模擬框架可用於ASP.NET MVC(您可以在此處查看它們[http://www.mockframeworks.com/](http://www.mockframeworks.com/)的清單:</span><span class="sxs-lookup"><span data-stu-id="f7b57-255">There are many .NET mocking frameworks that can be used with ASP.NET MVC (you can see a list of them here: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)).</span></span> <span data-ttu-id="f7b57-256">為了測試我們的NerdDinner應用程式,我們將使用一個開源類比框架,稱為"Moq",可以從[http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)免費下載 。</span><span class="sxs-lookup"><span data-stu-id="f7b57-256">For testing our NerdDinner application we'll use an open source mocking framework called "Moq", which can be downloaded for free from [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).</span></span>

<span data-ttu-id="f7b57-257">下載後,我們將在NerdDinner.測試專案中向Moq.dll程式集添加參考:</span><span class="sxs-lookup"><span data-stu-id="f7b57-257">Once downloaded, we'll add a reference in our NerdDinner.Tests project to the Moq.dll assembly:</span></span>

![](enable-automated-unit-testing/_static/image12.png)

<span data-ttu-id="f7b57-258">然後,我們將向測試類添加「創建 DinnerSControllerA(使用者名)」説明器方法,該方法以使用者名作為參數,然後「類比」DinnersController 實例上的User.Identity.Name屬性:</span><span class="sxs-lookup"><span data-stu-id="f7b57-258">We'll then add a "CreateDinnersControllerAs(username)" helper method to our test class that takes a username as a parameter, and which then "mocks" the User.Identity.Name property on the DinnersController instance:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

<span data-ttu-id="f7b57-259">上面,我們使用 Moq 創建一個模擬物件,該物件偽造了控制器上下文物件(ASP.NET MVC 傳遞給控制器類以公開運行時物件(如使用者、請求、回應和工作階段)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-259">Above we are using Moq to create a Mock object that fakes a ControllerContext object (which is what ASP.NET MVC passes to Controller classes to expose runtime objects like User, Request, Response, and Session).</span></span> <span data-ttu-id="f7b57-260">我們在 Mock 上調用「setupGet」方法,以指示 ControllerContext 上的HttpContext.User.Identity.Name屬性應返回我們傳遞給幫助器方法的使用者名字符串。</span><span class="sxs-lookup"><span data-stu-id="f7b57-260">We are calling the "SetupGet" method on the Mock to indicate that the HttpContext.User.Identity.Name property on ControllerContext should return the username string we passed to the helper method.</span></span>

<span data-ttu-id="f7b57-261">我們可以類比任意數量的控制器上下文屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="f7b57-261">We can mock any number of ControllerContext properties and methods.</span></span> <span data-ttu-id="f7b57-262">為了說明這一點,我還為 Request.Is 驗證屬性添加了 SetupGet() 調用(下面測試實際上不需要它,但這有助於說明如何模擬請求屬性)。</span><span class="sxs-lookup"><span data-stu-id="f7b57-262">To illustrate this I've also added a SetupGet() call for the Request.IsAuthenticated property (which isn't actually needed for the tests below – but which helps illustrate how you can mock Request properties).</span></span> <span data-ttu-id="f7b57-263">完成後,我們將控制器上下文類比的實例分配給 DinnersController,我們的幫助器方法返回。</span><span class="sxs-lookup"><span data-stu-id="f7b57-263">When we are done we assign an instance of the ControllerContext mock to the DinnersController our helper method returns.</span></span>

<span data-ttu-id="f7b57-264">現在,我們可以編寫使用此幫助器方法測試涉及不同使用者的編輯方案的單位測試:</span><span class="sxs-lookup"><span data-stu-id="f7b57-264">We can now write unit tests that use this helper method to test Edit scenarios involving different users:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

<span data-ttu-id="f7b57-265">現在,當我們運行測試時,他們通過:</span><span class="sxs-lookup"><span data-stu-id="f7b57-265">And now when we run the tests they pass:</span></span>

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a><span data-ttu-id="f7b57-266">測試更新模型()方案</span><span class="sxs-lookup"><span data-stu-id="f7b57-266">Testing UpdateModel() scenarios</span></span>

<span data-ttu-id="f7b57-267">我們創建了涵蓋"編輯"操作的 HTTP-GET 版本的測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-267">We've created tests that cover the HTTP-GET version of the Edit action.</span></span> <span data-ttu-id="f7b57-268">現在,讓我們創建一些測試來驗證編輯操作的 HTTP-POST 版本:</span><span class="sxs-lookup"><span data-stu-id="f7b57-268">Let's now create some tests that verify the HTTP-POST version of the Edit action:</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

<span data-ttu-id="f7b57-269">我們支援此操作方法的有趣新測試方案是它在 Controller 基類上使用 UpdateModel() 幫助器方法。</span><span class="sxs-lookup"><span data-stu-id="f7b57-269">The interesting new testing scenario for us to support with this action method is its usage of the UpdateModel() helper method on the Controller base class.</span></span> <span data-ttu-id="f7b57-270">我們使用此説明器方法將表單發佈值綁定到我們的 Dinner 物件實例。</span><span class="sxs-lookup"><span data-stu-id="f7b57-270">We are using this helper method to bind form-post values to our Dinner object instance.</span></span>

<span data-ttu-id="f7b57-271">下面是兩個測試,它們演示如何為 UpdateModel() 幫助器方法提供表單發佈值。</span><span class="sxs-lookup"><span data-stu-id="f7b57-271">Below are two tests that demonstrates how we can supply form posted values for the UpdateModel() helper method to use.</span></span> <span data-ttu-id="f7b57-272">我們將通過創建和填充 FormCollection 物件來執行此操作,然後將其分配給控制器上的"ValueProvider"屬性。</span><span class="sxs-lookup"><span data-stu-id="f7b57-272">We'll do this by creating and populating a FormCollection object, and then assign it to the "ValueProvider" property on the Controller.</span></span>

<span data-ttu-id="f7b57-273">第一個測試驗證在成功保存瀏覽器時是否重定向到詳細資訊操作。</span><span class="sxs-lookup"><span data-stu-id="f7b57-273">The first test verifies that on a successful save the browser is redirected to the details action.</span></span> <span data-ttu-id="f7b57-274">第二個測試驗證,當發佈無效輸入時,操作會再次用錯誤消息重新顯示編輯檢視。</span><span class="sxs-lookup"><span data-stu-id="f7b57-274">The second test verifies that when invalid input is posted the action redisplays the edit view again with an error message.</span></span>

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a><span data-ttu-id="f7b57-275">測試總結</span><span class="sxs-lookup"><span data-stu-id="f7b57-275">Testing Wrap-Up</span></span>

<span data-ttu-id="f7b57-276">我們介紹了單元測試控制器類中涉及的核心概念。</span><span class="sxs-lookup"><span data-stu-id="f7b57-276">We've covered the core concepts involved in unit testing controller classes.</span></span> <span data-ttu-id="f7b57-277">我們可以使用這些技術輕鬆創建數百個簡單的測試,以驗證我們應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="f7b57-277">We can use these techniques to easily create hundreds of simple tests that verify the behavior of our application.</span></span>

<span data-ttu-id="f7b57-278">由於我們的控制器和模型測試不需要真正的資料庫,因此它們非常快速且易於運行。</span><span class="sxs-lookup"><span data-stu-id="f7b57-278">Because our controller and model tests do not require a real database, they are extremely fast and easy to run.</span></span> <span data-ttu-id="f7b57-279">我們將能夠在數秒內執行數百個自動測試,並立即獲得反饋,了解我們所做的更改是否違反了某些內容。</span><span class="sxs-lookup"><span data-stu-id="f7b57-279">We'll be able to execute hundreds of automated tests in seconds, and immediately get feedback as to whether a change we made broke something.</span></span> <span data-ttu-id="f7b57-280">這將有助於我們有信心不斷改進、重構和改進我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b57-280">This will help provide us the confidence to continually improve, refactor, and refine our application.</span></span>

<span data-ttu-id="f7b57-281">我們將測試作為本章的最後一個主題進行介紹,但不是因為測試是您在開發過程結束時應該做的!</span><span class="sxs-lookup"><span data-stu-id="f7b57-281">We covered testing as the last topic in this chapter – but not because testing is something you should do at the end of a development process!</span></span> <span data-ttu-id="f7b57-282">相反,您應該在開發過程中儘早編寫自動化測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-282">On the contrary, you should write automated tests as early as possible in your development process.</span></span> <span data-ttu-id="f7b57-283">這樣做使您能夠在開發時立即獲得反饋,説明您仔細考慮應用程式的用例方案,並指導您設計應用程式時要牢記乾淨的分層和耦合。</span><span class="sxs-lookup"><span data-stu-id="f7b57-283">Doing so enables you to get immediate feedback as you develop, helps you think thoughtfully about your application's use case scenarios, and guides you to design your application with clean layering and coupling in mind.</span></span>

<span data-ttu-id="f7b57-284">本書的後一章將討論測試驅動開發 (TDD)以及如何將其與 mVC ASP.NET一起使用。</span><span class="sxs-lookup"><span data-stu-id="f7b57-284">A later chapter in the book will discuss Test Driven Development (TDD), and how to use it with ASP.NET MVC.</span></span> <span data-ttu-id="f7b57-285">TDD 是一種反覆運算碼實踐,您首先編寫生成的代碼將滿足的測試。</span><span class="sxs-lookup"><span data-stu-id="f7b57-285">TDD is an iterative coding practice where you first write the tests that your resulting code will satisfy.</span></span> <span data-ttu-id="f7b57-286">使用 TDD,您首先創建一個測試,以驗證即將實現的功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-286">With TDD you begin each feature by creating a test that verifies the functionality you are about to implement.</span></span> <span data-ttu-id="f7b57-287">首先編寫單元測試有助於確保您清楚地瞭解該功能及其應該如何工作。</span><span class="sxs-lookup"><span data-stu-id="f7b57-287">Writing the unit test first helps ensure that you clearly understand the feature and how it is supposed to work.</span></span> <span data-ttu-id="f7b57-288">只有在編寫測試(並且已驗證測試失敗)後,您才會實現測試驗證的實際功能。</span><span class="sxs-lookup"><span data-stu-id="f7b57-288">Only after the test is written (and you have verified that it fails) do you then implement the actual functionality the test verifies.</span></span> <span data-ttu-id="f7b57-289">由於您已經花時間考慮了該功能應該如何工作的用例,因此您將更好地瞭解這些要求以及如何最好地實現這些要求。</span><span class="sxs-lookup"><span data-stu-id="f7b57-289">Because you've already spent time thinking about the use case of how the feature is supposed to work, you will have a better understanding of the requirements and how best to implement them.</span></span> <span data-ttu-id="f7b57-290">完成實現後,您可以重新運行測試,並立即獲得有關該功能是否正常工作的反饋。</span><span class="sxs-lookup"><span data-stu-id="f7b57-290">When you are done with the implementation you can re-run the test – and get immediate feedback as to whether the feature works correctly.</span></span> <span data-ttu-id="f7b57-291">我們將在第 10 章中介紹 TDD。</span><span class="sxs-lookup"><span data-stu-id="f7b57-291">We'll cover TDD more in Chapter 10.</span></span>

### <a name="next-step"></a><span data-ttu-id="f7b57-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7b57-292">Next Step</span></span>

<span data-ttu-id="f7b57-293">一些最後的總結評論。</span><span class="sxs-lookup"><span data-stu-id="f7b57-293">Some final wrap up comments.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f7b57-294">[前一個](use-ajax-to-implement-mapping-scenarios.md)
> [下一個](nerddinner-wrap-up.md)</span><span class="sxs-lookup"><span data-stu-id="f7b57-294">[Previous](use-ajax-to-implement-mapping-scenarios.md)
[Next](nerddinner-wrap-up.md)</span></span>
