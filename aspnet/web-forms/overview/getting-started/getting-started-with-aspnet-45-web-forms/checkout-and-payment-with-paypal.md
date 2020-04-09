---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: 使用貝寶結帳和付款 |微軟文件
author: Erikre
description: 本教學系列將教您建構 ASP.NET Web 表單應用程式的基礎知識,使用ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80676052"
---
# <a name="checkout-and-payment-with-paypal"></a><span data-ttu-id="cc547-103">簽出與使用 PayPal 付款</span><span class="sxs-lookup"><span data-stu-id="cc547-103">Checkout and Payment with PayPal</span></span>

<span data-ttu-id="cc547-104">由[埃裡克·雷坦](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="cc547-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="cc547-105">[下載翼尖玩具樣品專案 (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="cc547-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="cc547-106">本教學系列將教您使用ASP.NET 4.5 和Microsoft Visual Studio Express 2013 為 Web 構建ASP.NET Web 表單應用程式的基礎知識。</span><span class="sxs-lookup"><span data-stu-id="cc547-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="cc547-107">帶有[C# 原始碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案可供本教學系列使用。</span><span class="sxs-lookup"><span data-stu-id="cc547-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="cc547-108">本教程介紹如何修改 Wingtip 玩具示例應用程式,以包括使用者授權、註冊和使用 PayPal 付款。</span><span class="sxs-lookup"><span data-stu-id="cc547-108">This tutorial describes how to modify the Wingtip Toys sample application to include user authorization, registration, and payment using PayPal.</span></span> <span data-ttu-id="cc547-109">只有登錄的使用者才有權購買產品。</span><span class="sxs-lookup"><span data-stu-id="cc547-109">Only users who are logged in will have authorization to purchase products.</span></span> <span data-ttu-id="cc547-110">ASP.NET 4.5 Web 窗體專案範本的內建用戶註冊功能已經包含了您需要的大部分內容。</span><span class="sxs-lookup"><span data-stu-id="cc547-110">The ASP.NET 4.5 Web Forms project template's built-in user registration functionality already includes much of what you need.</span></span> <span data-ttu-id="cc547-111">您將添加貝寶快速結帳功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-111">You will add PayPal Express Checkout functionality.</span></span> <span data-ttu-id="cc547-112">在本教學中,您使用的是PayPal開發者測試環境,因此不會轉移任何實際資金。</span><span class="sxs-lookup"><span data-stu-id="cc547-112">In this tutorial you be using the PayPal developer testing environment, so no actual funds will be transferred.</span></span> <span data-ttu-id="cc547-113">在本教程結束時,您將通過選擇要添加到購物車的產品、按一下結帳按鈕以及將數據傳輸到 PayPal 測試網站來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-113">At the end of the tutorial, you will test the application by selecting products to add to the shopping cart, clicking the checkout button, and transferring data to the PayPal testing web site.</span></span> <span data-ttu-id="cc547-114">在PayPal測試網站上,您將確認您的運費和付款資訊,然後返回當地的Wingtip玩具樣品應用程式,以確認和完成購買。</span><span class="sxs-lookup"><span data-stu-id="cc547-114">On the PayPal testing web site, you will confirm your shipping and payment information and then return to the local Wingtip Toys sample application to confirm and complete the purchase.</span></span>

<span data-ttu-id="cc547-115">有幾個經驗豐富的第三方支付處理器,專門從事在線購物,解決可擴展性和安全性。</span><span class="sxs-lookup"><span data-stu-id="cc547-115">There are several experienced third-party payment processors that specialize in online shopping that address scalability and security.</span></span> <span data-ttu-id="cc547-116">ASP.NET開發人員在實施購物和購買解決方案之前應考慮使用第三方支付解決方案的優勢。</span><span class="sxs-lookup"><span data-stu-id="cc547-116">ASP.NET developers should consider the advantages of utilizing a third party payment solution before implementing a shopping and purchasing solution.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc547-117">Wingtip Toys 示例應用程式旨在顯示ASP.NET網路開發人員可用的特定ASP.NET概念和功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-117">The Wingtip Toys sample application was designed to shown specific ASP.NET concepts and features available to ASP.NET web developers.</span></span> <span data-ttu-id="cc547-118">此示例應用程式未針對可擴充性和安全性方面的所有可能情況進行優化。</span><span class="sxs-lookup"><span data-stu-id="cc547-118">This sample application was not optimized for all possible circumstances in regard to scalability and security.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="cc547-119">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="cc547-119">What you'll learn:</span></span>

- <span data-ttu-id="cc547-120">如何限制對資料夾中特定頁面的訪問。</span><span class="sxs-lookup"><span data-stu-id="cc547-120">How to restrict access to specific pages in a folder.</span></span>
- <span data-ttu-id="cc547-121">如何從匿名購物車創建已知的購物車。</span><span class="sxs-lookup"><span data-stu-id="cc547-121">How to create a known shopping cart from an anonymous shopping cart.</span></span>
- <span data-ttu-id="cc547-122">如何為項目啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="cc547-122">How to enable SSL for the project.</span></span>
- <span data-ttu-id="cc547-123">如何向專案添加 OAuth 提供程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-123">How to add an OAuth provider to the project.</span></span>
- <span data-ttu-id="cc547-124">如何使用PayPal使用PayPal測試環境購買產品。</span><span class="sxs-lookup"><span data-stu-id="cc547-124">How to use PayPal to purchase products using the PayPal testing environment.</span></span>
- <span data-ttu-id="cc547-125">如何在**詳細資訊查看**控件中顯示來自 PayPal 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-125">How to display details from PayPal in a **DetailsView** control.</span></span>
- <span data-ttu-id="cc547-126">如何更新翼尖玩具應用程序的資料庫與從PayPal獲得的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-126">How to update the database of the Wingtip Toys application with details obtained from PayPal.</span></span>

## <a name="adding-order-tracking"></a><span data-ttu-id="cc547-127">新增訂單追蹤</span><span class="sxs-lookup"><span data-stu-id="cc547-127">Adding Order Tracking</span></span>

<span data-ttu-id="cc547-128">在本教學中,您將創建兩個新類來追蹤用戶創建的順序中的數據。</span><span class="sxs-lookup"><span data-stu-id="cc547-128">In this tutorial, you'll create two new classes to track data from the order a user has created.</span></span> <span data-ttu-id="cc547-129">這些課程將跟蹤有關運輸資訊、採購總額和付款確認的數據。</span><span class="sxs-lookup"><span data-stu-id="cc547-129">The classes will track data regarding shipping information, purchase total, and payment confirmation.</span></span>

### <a name="add-the-order-and-orderdetail-model-classes"></a><span data-ttu-id="cc547-130">新增訂單及訂單詳細資訊模型類別</span><span class="sxs-lookup"><span data-stu-id="cc547-130">Add the Order and OrderDetail Model Classes</span></span>

<span data-ttu-id="cc547-131">在本教學系列的早期,透過*在 「模型」* 資料夾`Category`中`Product`創建`CartItem`、 類別,定義類別、產品和購物車專案的架構。</span><span class="sxs-lookup"><span data-stu-id="cc547-131">Earlier in this tutorial series, you defined the schema for categories, products, and shopping cart items by creating the `Category`, `Product`, and `CartItem` classes in the *Models* folder.</span></span> <span data-ttu-id="cc547-132">現在,您將添加兩個新類來定義產品訂單的架構和訂單的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-132">Now you will add two new classes to define the schema for the product order and the details of the order.</span></span>

1. <span data-ttu-id="cc547-133">在**模型「 資料夾**中,添加名為*Order.cs*的新類。</span><span class="sxs-lookup"><span data-stu-id="cc547-133">In the **Models** folder, add a new class named *Order.cs*.</span></span>   
   <span data-ttu-id="cc547-134">新的類文件顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="cc547-134">The new class file is displayed in the editor.</span></span>
2. <span data-ttu-id="cc547-135">使用下列項目取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="cc547-135">Replace the default code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. <span data-ttu-id="cc547-136">將*OrderDetail.cs*類別加入*模型的資料夾*。</span><span class="sxs-lookup"><span data-stu-id="cc547-136">Add an *OrderDetail.cs* class to the *Models* folder.</span></span>
4. <span data-ttu-id="cc547-137">使用下列程式碼來取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="cc547-137">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

<span data-ttu-id="cc547-138">`Order`和`OrderDetail`類包含用於定義用於採購和裝運的訂單資訊的架構。</span><span class="sxs-lookup"><span data-stu-id="cc547-138">The `Order` and `OrderDetail` classes contain the schema to define the order information used for purchasing and shipping.</span></span>

<span data-ttu-id="cc547-139">此外,您需要更新管理實體類並提供對資料庫的數據訪問的資料庫上下文類。</span><span class="sxs-lookup"><span data-stu-id="cc547-139">In addition, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="cc547-140">為此,您將新創建的 Order`OrderDetail`和模型類`ProductContext`添加到 類中。</span><span class="sxs-lookup"><span data-stu-id="cc547-140">To do this, you will add the newly created Order and `OrderDetail` model classes to `ProductContext` class.</span></span>

1. <span data-ttu-id="cc547-141">在**解決方案資源管理員中**,尋找*並開啟ProductContext.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="cc547-141">In **Solution Explorer**, find and open the *ProductContext.cs* file.</span></span>
2. <span data-ttu-id="cc547-142">將突顯的代碼加入*ProductContext.cs*檔案,如下所示:</span><span class="sxs-lookup"><span data-stu-id="cc547-142">Add the highlighted code to the *ProductContext.cs* file as shown below:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

<span data-ttu-id="cc547-143">如本教學系列前面所述 *,ProductContext.cs*檔案中的`System.Data.Entity`代碼添加 命名空間,以便您可以存取實體框架的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-143">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="cc547-144">此功能包括透過使用強類型物件來查詢、插入、更新和刪除資料的功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-144">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="cc547-145">類中的`ProductContext`上述代碼增加了實體框架對新`Order`添加 的`OrderDetail`類和 類的訪問。</span><span class="sxs-lookup"><span data-stu-id="cc547-145">The above code in the `ProductContext` class adds Entity Framework access to the newly added `Order` and `OrderDetail` classes.</span></span>

## <a name="adding-checkout-access"></a><span data-ttu-id="cc547-146">新增簽出存取權限</span><span class="sxs-lookup"><span data-stu-id="cc547-146">Adding Checkout Access</span></span>

<span data-ttu-id="cc547-147">Wingtip玩具範例應用程式允許匿名使用者查看產品並將其添加到購物車中。</span><span class="sxs-lookup"><span data-stu-id="cc547-147">The Wingtip Toys sample application allows anonymous users to review and add products to a shopping cart.</span></span> <span data-ttu-id="cc547-148">但是,當匿名用戶選擇購買他們添加到購物車的產品時,他們必須登錄到網站。</span><span class="sxs-lookup"><span data-stu-id="cc547-148">However, when anonymous users choose to purchase the products they added to the shopping cart, they must log on to the site.</span></span> <span data-ttu-id="cc547-149">登錄後,他們可以存取處理結帳和購買過程的 Web 應用程式的受限頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-149">Once they have logged on, they can access the restricted pages of the Web application that handle the checkout and purchase process.</span></span> <span data-ttu-id="cc547-150">這些受限頁面包含在應用程式的*簽出*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="cc547-150">These restricted pages are contained in the *Checkout* folder of the application.</span></span>

### <a name="add-a-checkout-folder-and-pages"></a><span data-ttu-id="cc547-151">新增結帳資料夾與頁面</span><span class="sxs-lookup"><span data-stu-id="cc547-151">Add a Checkout Folder and Pages</span></span>

<span data-ttu-id="cc547-152">現在,您將創建 *「簽出*」資料夾以及客戶在結帳過程中將看到的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-152">You will now create the *Checkout* folder and the pages in it that the customer will see during the checkout process.</span></span> <span data-ttu-id="cc547-153">本教程稍後將更新這些頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-153">You will update these pages later in this tutorial.</span></span>

1. <span data-ttu-id="cc547-154">右鍵按一下**解決方案資源管理器**中的專案名稱 (**翼尖玩具**) 並選擇 **「添加新資料夾**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-154">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add a New Folder**.</span></span> 

    ![使用 PayPal 結帳和付款 - 新資料夾](checkout-and-payment-with-paypal/_static/image1.png)
2. <span data-ttu-id="cc547-156">已命名新資料夾*簽出*。</span><span class="sxs-lookup"><span data-stu-id="cc547-156">Name the new folder *Checkout*.</span></span>
3. <span data-ttu-id="cc547-157">右鍵按下*簽出*資料夾,然後選擇「**添加新**-&gt;**專案**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-157">Right-click the *Checkout* folder and then select **Add**-&gt;**New Item**.</span></span> 

    ![使用PayPal結帳和付款 - 新專案](checkout-and-payment-with-paypal/_static/image2.png)
4. <span data-ttu-id="cc547-159">[ **加入新項目** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cc547-159">The **Add New Item** dialog box is displayed.</span></span>
5. <span data-ttu-id="cc547-160">選擇左側的**可視化 C#**  - &gt; **Web**範本組。</span><span class="sxs-lookup"><span data-stu-id="cc547-160">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="cc547-161">然後,從中間窗格中,選擇**帶有母版頁的 Web 窗體**並將其命名為 *「簽出Start.aspx*」。</span><span class="sxs-lookup"><span data-stu-id="cc547-161">Then, from the middle pane, select **Web Form with Master Page**and name it *CheckoutStart.aspx*.</span></span> 

    ![使用 PayPal 結帳和付款 - 新增新項目對話框](checkout-and-payment-with-paypal/_static/image3.png)
6. <span data-ttu-id="cc547-163">與之前一樣,選擇*Site.Master*檔作為母版頁。</span><span class="sxs-lookup"><span data-stu-id="cc547-163">As before, select the *Site.Master* file as the master page.</span></span>
7. <span data-ttu-id="cc547-164">使用上述相同的步驟將以下其他頁面加入*到 簽出*資料夾:</span><span class="sxs-lookup"><span data-stu-id="cc547-164">Add the following additional pages to the *Checkout* folder using the same steps above:</span></span>   

    - <span data-ttu-id="cc547-165">簽出審查.aspx</span><span class="sxs-lookup"><span data-stu-id="cc547-165">CheckoutReview.aspx</span></span>
    - <span data-ttu-id="cc547-166">結帳完成.aspx</span><span class="sxs-lookup"><span data-stu-id="cc547-166">CheckoutComplete.aspx</span></span>
    - <span data-ttu-id="cc547-167">結帳取消.aspx</span><span class="sxs-lookup"><span data-stu-id="cc547-167">CheckoutCancel.aspx</span></span>
    - <span data-ttu-id="cc547-168">結帳錯誤.aspx</span><span class="sxs-lookup"><span data-stu-id="cc547-168">CheckoutError.aspx</span></span>

### <a name="add-a-webconfig-file"></a><span data-ttu-id="cc547-169">新增 Web.config 檔案</span><span class="sxs-lookup"><span data-stu-id="cc547-169">Add a Web.config File</span></span>

<span data-ttu-id="cc547-170">以將新的*Web.config*檔案加入*到 簽出*資料夾,您將能夠限制對資料夾中包含的所有頁面的存取。</span><span class="sxs-lookup"><span data-stu-id="cc547-170">By adding a new *Web.config* file to the *Checkout* folder, you will be able to restrict access to all the pages contained in the folder.</span></span>

1. <span data-ttu-id="cc547-171">右鍵按一*下 簽出*資料夾並選擇「**新增新** -&gt;**專案**」。。</span><span class="sxs-lookup"><span data-stu-id="cc547-171">Right-click the *Checkout* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="cc547-172">[ **加入新項目** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cc547-172">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="cc547-173">選擇左側的**可視化 C#**  - &gt; **Web**範本組。</span><span class="sxs-lookup"><span data-stu-id="cc547-173">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="cc547-174">然後,從中間窗格中,選擇**Web 設定檔**,接受*Web.config*的預設名稱,然後選擇 **「添加**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-174">Then, from the middle pane, select **Web Configuration File**, accept the default name of *Web.config*, and then select **Add**.</span></span>
3. <span data-ttu-id="cc547-175">使用下列內容來取代 *Web.config* 檔案中的現有 XML 內容：</span><span class="sxs-lookup"><span data-stu-id="cc547-175">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. <span data-ttu-id="cc547-176">儲存 *Web.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="cc547-176">Save the *Web.config* file.</span></span>

<span data-ttu-id="cc547-177">*Web.config 檔案*指定必須拒絕 Web 應用程式的所有未知使用者存*取 簽出*資料夾中的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-177">The *Web.config* file specifies that all unknown users of the Web application must be denied access to the pages contained in the *Checkout* folder.</span></span> <span data-ttu-id="cc547-178">但是,如果使用者已註冊了帳戶並登錄了帳戶,則他們將是已知使用者,並有權訪問 *「簽出」* 資料夾中的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-178">However, if the user has registered an account and is logged on, they will be a known user and will have access to the pages in the *Checkout* folder.</span></span>

<span data-ttu-id="cc547-179">請務必注意,ASP.NET配置遵循層次結構,其中每個*Web.config*檔將配置設置應用於它所在的資料夾及其下的所有子目錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-179">It's important to note that ASP.NET configuration follows a hierarchy, where each *Web.config* file applies configuration settings to the folder that it is in and to all of the child directories below it.</span></span>

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a><span data-ttu-id="cc547-180">對專案啟用 SSL</span><span class="sxs-lookup"><span data-stu-id="cc547-180">Enable SSL for the Project</span></span>

 <span data-ttu-id="cc547-181">安全通訊端層 (SSL) 是一種定義的通訊協定，允許 Web 伺服器和 Web 用戶端透過加密，以更安全的方式進行通訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-181">Secure Sockets Layer (SSL) is a protocol defined to allow Web servers and Web clients to communicate more securely through the use of encryption.</span></span> <span data-ttu-id="cc547-182">未使用 SSL 時，在用戶端和伺服器之間傳送的資料會開放給任何可實體存取網路的人員進行封包探查。</span><span class="sxs-lookup"><span data-stu-id="cc547-182">When SSL is not used, data sent between the client and server is open to packet sniffing by anyone with physical access to the network.</span></span> <span data-ttu-id="cc547-183">此外，數種常見驗證結構描述在一般的 HTTP 上並不是很安全。</span><span class="sxs-lookup"><span data-stu-id="cc547-183">Additionally, several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="cc547-184">尤其是，基本驗證和表單驗證會傳送未加密的認證。</span><span class="sxs-lookup"><span data-stu-id="cc547-184">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="cc547-185">為了安全的理由，這些驗證結構描述必須使用 SSL。</span><span class="sxs-lookup"><span data-stu-id="cc547-185">To be secure, these authentication schemes must use SSL.</span></span> 

1. <span data-ttu-id="cc547-186">在 **「解決方案資源管理器」** 中,按**一下 WingtipToys**專案,然後按**F4**顯示 **「屬性」** 視窗。</span><span class="sxs-lookup"><span data-stu-id="cc547-186">In **Solution Explorer**, click the **WingtipToys** project, then press **F4** to display the **Properties** window.</span></span>
2. <span data-ttu-id="cc547-187">將**SSL**`true`變更為 。</span><span class="sxs-lookup"><span data-stu-id="cc547-187">Change **SSL Enabled** to `true`.</span></span>
3. <span data-ttu-id="cc547-188">複製 **SSL URL** ，以便稍後使用。</span><span class="sxs-lookup"><span data-stu-id="cc547-188">Copy the **SSL URL** so you can use it later.</span></span>   
 <span data-ttu-id="cc547-189">SSL URL`https://localhost:44300/`將是 除非您以前創建了 SSL 網站(如下所示)。</span><span class="sxs-lookup"><span data-stu-id="cc547-189">The SSL URL will be `https://localhost:44300/` unless you've previously created SSL Web Sites (as shown below).</span></span>   
    <span data-ttu-id="cc547-190">![專案屬性](checkout-and-payment-with-paypal/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-190">![Project Properties](checkout-and-payment-with-paypal/_static/image4.png)</span></span>
4. <span data-ttu-id="cc547-191">在**解決方案資源管理員**中,右鍵按**一下 WingtipToys**專案,然後按下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="cc547-191">In **Solution Explorer**, right click the **WingtipToys** project and click **Properties**.</span></span>
5. <span data-ttu-id="cc547-192">在左側索引標籤中按一下 [Web] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="cc547-192">In the left tab, click **Web**.</span></span>
6. <span data-ttu-id="cc547-193">變更**專案網址**以使用之前保存的**SSL URL。**</span><span class="sxs-lookup"><span data-stu-id="cc547-193">Change the **Project Url** to use the **SSL URL** that you saved earlier.</span></span>   
    <span data-ttu-id="cc547-194">![專案 Web 屬性](checkout-and-payment-with-paypal/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-194">![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)</span></span>
7. <span data-ttu-id="cc547-195">按 **CTRL+S**儲存頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-195">Save the page by pressing **CTRL+S**.</span></span>
8. <span data-ttu-id="cc547-196">按**Ctrl+F5**以運行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-196">Press **Ctrl+F5** to run the application.</span></span> <span data-ttu-id="cc547-197">Visual Studio 將會顯示可避開 SSL 警告的選項。</span><span class="sxs-lookup"><span data-stu-id="cc547-197">Visual Studio will display an option to allow you to avoid SSL warnings.</span></span>
9. <span data-ttu-id="cc547-198">按一下 [ **是** ] 以信任 IIS Express SSL 憑證並繼續。</span><span class="sxs-lookup"><span data-stu-id="cc547-198">Click **Yes** to trust the IIS Express SSL certificate and continue.</span></span>   
    <span data-ttu-id="cc547-199">![IIS Express SSL 憑證資訊](checkout-and-payment-with-paypal/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-199">![IIS Express SSL certificate details](checkout-and-payment-with-paypal/_static/image6.png)</span></span>  
 <span data-ttu-id="cc547-200"> 隨即顯示一則安全性警告。</span><span class="sxs-lookup"><span data-stu-id="cc547-200">A Security Warning is displayed.</span></span>
10. <span data-ttu-id="cc547-201">按一下 [ **是** ] 將憑證安裝到您的 localhost。</span><span class="sxs-lookup"><span data-stu-id="cc547-201">Click **Yes** to install the certificate to your localhost.</span></span>   
    <span data-ttu-id="cc547-202">![[安全性警告] 對話方塊](checkout-and-payment-with-paypal/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-202">![Security Warning dialog box](checkout-and-payment-with-paypal/_static/image7.png)</span></span>  
 <span data-ttu-id="cc547-203"> 瀏覽器視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cc547-203">The browser window will be displayed.</span></span>

<span data-ttu-id="cc547-204">現在,您可以使用 SSL 在本地輕鬆測試 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-204">You can now easily test your Web application locally using SSL.</span></span>

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a><span data-ttu-id="cc547-205">新增 OAuth 2.0 提供者</span><span class="sxs-lookup"><span data-stu-id="cc547-205">Add an OAuth 2.0 Provider</span></span>

<span data-ttu-id="cc547-206">ASP.NET Web Forms 提供成員資格和驗證的增強功能選項。</span><span class="sxs-lookup"><span data-stu-id="cc547-206">ASP.NET Web Forms provides enhanced options for membership and authentication.</span></span> <span data-ttu-id="cc547-207">這些增強功能包括 OAuth。</span><span class="sxs-lookup"><span data-stu-id="cc547-207">These enhancements include OAuth.</span></span> <span data-ttu-id="cc547-208">OAuth 是一種開放式通訊協定，可讓 Web、行動和桌面應用程式以簡單、標準的方法執行安全授權。</span><span class="sxs-lookup"><span data-stu-id="cc547-208">OAuth is an open protocol that allows secure authorization in a simple and standard method from web, mobile, and desktop applications.</span></span> <span data-ttu-id="cc547-209">ASP.NET Web 表單範本使用 OAuth 公開 Facebook、Twitter、Google 和微軟作為身份驗證供應商。</span><span class="sxs-lookup"><span data-stu-id="cc547-209">The ASP.NET Web Forms template uses OAuth to expose Facebook, Twitter, Google and Microsoft as authentication providers.</span></span> <span data-ttu-id="cc547-210">雖然本教學課程僅使用 Google 作為驗證提供者，但您可以輕易修改程式碼來使用任何提供者。</span><span class="sxs-lookup"><span data-stu-id="cc547-210">Although this tutorial uses only Google as the authentication provider, you can easily modify the code to use any of the providers.</span></span> <span data-ttu-id="cc547-211">實作其他提供者的步驟，與您將在本教學課程中看到的步驟極為類似。</span><span class="sxs-lookup"><span data-stu-id="cc547-211">The steps to implement other providers are very similar to the steps you will see in this tutorial.</span></span>

<span data-ttu-id="cc547-212">除了驗證，本教學課程也會使用角色來實作授權。</span><span class="sxs-lookup"><span data-stu-id="cc547-212">In addition to authentication, the tutorial will also use roles to implement authorization.</span></span> <span data-ttu-id="cc547-213">只有您新增至 `canEdit` 角色的使用者才能建立、編輯或刪除連絡人。</span><span class="sxs-lookup"><span data-stu-id="cc547-213">Only those users you add to the `canEdit` role will be able to change data (create, edit, or delete contacts).</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc547-214">Windows Live 應用程式僅接受工作網站的即時 URL,因此不能使用本地網站 URL 來測試登錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-214">Windows Live applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>

<span data-ttu-id="cc547-215">下列步驟可新增 Google 驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="cc547-215">The following steps will allow you to add a Google authentication provider.</span></span>

1. <span data-ttu-id="cc547-216">打開*\_應用啟動\啟動.Auth.cs*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-216">Open the *App\_Start\Startup.Auth.cs* file.</span></span>
2. <span data-ttu-id="cc547-217">移除 `app.UseGoogleAuthentication()` 方法中的註解字元，然後此方法會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="cc547-217">Remove the comment characters from the `app.UseGoogleAuthentication()` method so that the method appears as follows:</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. <span data-ttu-id="cc547-218">瀏覽至 [Google Developers Console](https://console.developers.google.com/)。</span><span class="sxs-lookup"><span data-stu-id="cc547-218">Navigate to the [Google Developers Console](https://console.developers.google.com/).</span></span> <span data-ttu-id="cc547-219">您還需要使用您的 Google 開發人員電子郵件帳戶 (gmail.com) 登入。</span><span class="sxs-lookup"><span data-stu-id="cc547-219">You will also need to sign-in with your Google developer email account (gmail.com).</span></span> <span data-ttu-id="cc547-220">如果您沒有 Google 帳戶，請選取 [ **建立帳戶** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="cc547-220">If you do not have a Google account, select the **Create an account** link.</span></span>   
   <span data-ttu-id="cc547-221">接下來，您會看到 [ **Google 開發人員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="cc547-221">Next, you'll see the **Google Developers Console**.</span></span>   
    <span data-ttu-id="cc547-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-222">![Google Developers Console](checkout-and-payment-with-paypal/_static/image8.png)</span></span>
4. <span data-ttu-id="cc547-223">按下「**建立專案**」 按鈕並輸入專案名稱和 ID(您可以使用預設值)。</span><span class="sxs-lookup"><span data-stu-id="cc547-223">Click the **Create Project** button and enter a project name and ID (you can use the default values).</span></span> <span data-ttu-id="cc547-224">然後,按一**下協定複選框**和 **「創建**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-224">Then, click the **agreement checkbox** and the **Create** button.</span></span>  

    ![谷歌 - 新專案](checkout-and-payment-with-paypal/_static/image9.png)

   <span data-ttu-id="cc547-226"> 幾秒鐘內即可建立新的專案，您的瀏覽器便會顯示新的專案頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-226">In a few seconds the new project will be created and your browser will display the new projects page.</span></span>
5. <span data-ttu-id="cc547-227">在左方選項卡中,按下**API &amp; auth,** 然後按下**認證 。**</span><span class="sxs-lookup"><span data-stu-id="cc547-227">In the left tab, click **APIs &amp; auth**, and then click **Credentials**.</span></span>
6. <span data-ttu-id="cc547-228">按一下**OAuth**下的**建立新用戶端 ID。**</span><span class="sxs-lookup"><span data-stu-id="cc547-228">Click the **Create New Client ID** under **OAuth**.</span></span>   
   <span data-ttu-id="cc547-229">[ **建立用戶端識別碼** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cc547-229">The **Create Client ID** dialog will be displayed.</span></span>   
    <span data-ttu-id="cc547-230">![Google -  建立用戶端識別碼](checkout-and-payment-with-paypal/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-230">![Google - Create Client ID](checkout-and-payment-with-paypal/_static/image10.png)</span></span>
7. <span data-ttu-id="cc547-231">在 **"建立用戶端 ID'** 對話框中,保留應用程式類型的預設**Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cc547-231">In the **Create Client ID** dialog, keep the default **Web application** for the application type.</span></span>
8. <span data-ttu-id="cc547-232">將**授權的 JavaScript 源**設定為本教學前面使用的`https://localhost:44300/`SSL 網址( 除非您建立了其他 SSL 專案)。</span><span class="sxs-lookup"><span data-stu-id="cc547-232">Set the **Authorized JavaScript Origins** to the SSL URL you used earlier in this tutorial (`https://localhost:44300/` unless you've created other SSL projects).</span></span>   
   <span data-ttu-id="cc547-233">此 URL 會是應用程式的原始來源。</span><span class="sxs-lookup"><span data-stu-id="cc547-233">This URL is the origin for your application.</span></span> <span data-ttu-id="cc547-234">在此範例中，您將僅輸入 localhost 測試 URL。</span><span class="sxs-lookup"><span data-stu-id="cc547-234">For this sample, you will only enter the localhost test URL.</span></span> <span data-ttu-id="cc547-235">但是,您可以輸入多個 URL 來考慮本地主機和生產。</span><span class="sxs-lookup"><span data-stu-id="cc547-235">However, you can enter multiple URLs to account for localhost and production.</span></span>
9. <span data-ttu-id="cc547-236">將 [Authorized Redirect URI] \*\*\*\* 設定如下：</span><span class="sxs-lookup"><span data-stu-id="cc547-236">Set the **Authorized Redirect URI** to the following:</span></span> 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   <span data-ttu-id="cc547-237">此值是 ASP.NET OAuth 使用者與 Google OAuth 伺服器進行通訊的 URI。</span><span class="sxs-lookup"><span data-stu-id="cc547-237">This value is the URI that ASP.NET OAuth users to communicate with the google OAuth server.</span></span> <span data-ttu-id="cc547-238">請記住上面使用的 SSL`https://localhost:44300/`網址( 除非您創建了其他 SSL 專案)。</span><span class="sxs-lookup"><span data-stu-id="cc547-238">Remember the SSL URL you used above (    `https://localhost:44300/` unless you've created other SSL projects).</span></span>
10. <span data-ttu-id="cc547-239">按下「**創建用戶端 ID」** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-239">Click the **Create Client ID** button.</span></span>
11. <span data-ttu-id="cc547-240">在 Google 開發人員控制台的左側功能表中,按一下 **「同意「螢幕**功能表項,然後設定您的電子郵寄地址和產品名稱。</span><span class="sxs-lookup"><span data-stu-id="cc547-240">On the left menu of the Google Developers Console, click the **Consent screen** menu item, then set your email address and product name.</span></span> <span data-ttu-id="cc547-241">填寫完表單後,按一下「**保存**」。。</span><span class="sxs-lookup"><span data-stu-id="cc547-241">When you have completed the form, click **Save**.</span></span>
12. <span data-ttu-id="cc547-242">按**下 API**選單項,向下滾動並按**下 Google+ API**旁邊的**關閉**按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-242">Click the **APIs** menu item, scroll down and click the **off** button next to **Google+ API**.</span></span>   
    <span data-ttu-id="cc547-243">接受此選項將啟用 Google+ API。</span><span class="sxs-lookup"><span data-stu-id="cc547-243">Accepting this option will enable the Google+ API.</span></span>
13. <span data-ttu-id="cc547-244">您還必須將**Microsoft.Owin** NuGet 包更新為 3.0.0 版。</span><span class="sxs-lookup"><span data-stu-id="cc547-244">You must also update the **Microsoft.Owin** NuGet package to version 3.0.0.</span></span>   
    <span data-ttu-id="cc547-245">從**工具選**單中,選擇**NuGet 套件管理員**,然後選擇 **「管理解決方案的 NuGet 套件**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-245">From the **Tools** menu, select **NuGet Package Manager** and then select **Manage NuGet Packages for Solution**.</span></span>  
    <span data-ttu-id="cc547-246">從 **「管理 NuGet 包」** 視窗中尋找**Microsoft.Owin**套件並將其更新為版本 3.0.0。</span><span class="sxs-lookup"><span data-stu-id="cc547-246">From the **Manage NuGet Packages** window, find and update the **Microsoft.Owin** package to version 3.0.0.</span></span>
14. <span data-ttu-id="cc547-247">在`UseGoogleAuthentication`Visual Studio 中,通過將 用戶端**ID**和**用戶端機密**複製並貼上到方法中,更新*Startup.Auth.cs*頁的方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-247">In Visual Studio, update the `UseGoogleAuthentication` method of the *Startup.Auth.cs* page by copying and pasting the **Client ID** and **Client Secret** into the method.</span></span> <span data-ttu-id="cc547-248">下面顯示**的用戶端 ID**和**用戶端機密**值是示例,不起作用。</span><span class="sxs-lookup"><span data-stu-id="cc547-248">The **Client ID** and **Client Secret** values shown below are samples and will not work.</span></span> 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. <span data-ttu-id="cc547-249">按**CTRL+F5**生成並運行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-249">Press **CTRL+F5** to build and run the application.</span></span> <span data-ttu-id="cc547-250">按一下 [登入] \*\*\*\* 連結。</span><span class="sxs-lookup"><span data-stu-id="cc547-250">Click the **Log in** link.</span></span>
16. <span data-ttu-id="cc547-251">在 **「使用其他服務登入**」下,按**一下 Google**。</span><span class="sxs-lookup"><span data-stu-id="cc547-251">Under **Use another service to log in**, click **Google**.</span></span>  
    <span data-ttu-id="cc547-252">![登入](checkout-and-payment-with-paypal/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-252">![Log in](checkout-and-payment-with-paypal/_static/image11.png)</span></span>
17. <span data-ttu-id="cc547-253">如果您需要輸入認證，您會被重新導向至 Google 網站，您可以在此輸入認證。</span><span class="sxs-lookup"><span data-stu-id="cc547-253">If you need to enter your credentials, you will be redirected to the google site where you will enter your credentials.</span></span>  
    ![Google - 登入](checkout-and-payment-with-paypal/_static/image12.png)
18. <span data-ttu-id="cc547-255">輸入認證後,系統將提示您向剛剛建立的 Web 應用程式授予許可權。</span><span class="sxs-lookup"><span data-stu-id="cc547-255">After you enter your credentials, you will be prompted to give permissions to the web application you just created.</span></span>  
    ![專案預設服務帳戶](checkout-and-payment-with-paypal/_static/image13.png)
19. <span data-ttu-id="cc547-257">按下"**接受**"。</span><span class="sxs-lookup"><span data-stu-id="cc547-257">Click **Accept**.</span></span> <span data-ttu-id="cc547-258">現在,您將被重定向回**WingtipToys**應用程式的**註冊**頁面,您可以在其中註冊您的 Google 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-258">You will now be redirected back to the **Register** page of the **WingtipToys** application where you can register your Google account.</span></span>  
    <span data-ttu-id="cc547-259">![以您的 Google 帳戶註冊](checkout-and-payment-with-paypal/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="cc547-259">![Register with your Google Account](checkout-and-payment-with-paypal/_static/image14.png)</span></span>
20. <span data-ttu-id="cc547-260">您可以選擇變更用於 Gmail 帳戶的本機電子郵件註冊名稱，但您通常會想保留預設電子郵件別名 (也就是，您用來驗證的名稱)。</span><span class="sxs-lookup"><span data-stu-id="cc547-260">You have the option of changing the local email registration name used for your Gmail account, but you generally want to keep the default email alias (that is, the one you used for authentication).</span></span> <span data-ttu-id="cc547-261">點選**上所述的登入**。</span><span class="sxs-lookup"><span data-stu-id="cc547-261">Click **Log in** as shown above.</span></span>

### <a name="modifying-login-functionality"></a><span data-ttu-id="cc547-262">變更登入功能</span><span class="sxs-lookup"><span data-stu-id="cc547-262">Modifying Login Functionality</span></span>

<span data-ttu-id="cc547-263">如本教學系列前面所述,預設情況下,ASP.NET Web 窗體範本中已包含許多用戶註冊功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-263">As previously mentioned in this tutorial series, much of the user registration functionality has been included in the ASP.NET Web Forms template by default.</span></span> <span data-ttu-id="cc547-264">現在,您將修改預設*的 Login.aspx*和*Register.aspx*`MigrateCart`頁面來調用該方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-264">Now you will modify the default *Login.aspx* and *Register.aspx* pages to call the `MigrateCart` method.</span></span> <span data-ttu-id="cc547-265">該方法`MigrateCart`將新登錄的使用者與匿名購物車關聯。</span><span class="sxs-lookup"><span data-stu-id="cc547-265">The `MigrateCart` method associates a newly logged in user with an anonymous shopping cart.</span></span> <span data-ttu-id="cc547-266">通過將使用者和購物車關聯,Wingtip 玩具示例應用程式將能夠在訪問之間維護用戶的購物車。</span><span class="sxs-lookup"><span data-stu-id="cc547-266">By associating the user and shopping cart, the Wingtip Toys sample application will be able to maintain the shopping cart of the user between visits.</span></span>

1. <span data-ttu-id="cc547-267">在**解決方案資源管理員中**,尋找 *「帳戶」* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc547-267">In **Solution Explorer**, find and open the *Account* folder.</span></span>
2. <span data-ttu-id="cc547-268">修改名為*Login.aspx.cs*的代碼後面頁,以包括以黃色突出顯示的代碼,以便如下所示:</span><span class="sxs-lookup"><span data-stu-id="cc547-268">Modify the code-behind page named *Login.aspx.cs* to include the code highlighted in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. <span data-ttu-id="cc547-269">保存*Login.aspx.cs*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-269">Save the *Login.aspx.cs* file.</span></span>

<span data-ttu-id="cc547-270">現在,您可以忽略方法沒有定義的警告`MigrateCart`。</span><span class="sxs-lookup"><span data-stu-id="cc547-270">For now, you can ignore the warning that there is no definition for the `MigrateCart` method.</span></span> <span data-ttu-id="cc547-271">您將在本教程稍後添加它。</span><span class="sxs-lookup"><span data-stu-id="cc547-271">You will be adding it a bit later in this tutorial.</span></span>

<span data-ttu-id="cc547-272">*Login.aspx.cs*代碼背後的文件支援登錄方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-272">The *Login.aspx.cs* code-behind file supports a LogIn method.</span></span> <span data-ttu-id="cc547-273">通過檢查 Login.aspx 頁面,您將看到此頁面包含一個「登錄」按鈕,按下該按鈕會在代碼`LogIn`後面的 處理程式觸發該按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-273">By inspecting the Login.aspx page, you'll see that this page includes a "Log in" button that when click triggers the `LogIn` handler on the code-behind.</span></span>

<span data-ttu-id="cc547-274">呼叫Login.aspx.cs`Login`上的方法*Login.aspx.cs*時,將創建`usersShoppingCart`名為購物車的新實例。</span><span class="sxs-lookup"><span data-stu-id="cc547-274">When the `Login` method on the *Login.aspx.cs* is called, a new instance of the shopping cart named `usersShoppingCart` is created.</span></span> <span data-ttu-id="cc547-275">購物車 (GUID) 的 ID 將檢`cartId`索並設置為 變數。</span><span class="sxs-lookup"><span data-stu-id="cc547-275">The ID of the shopping cart (a GUID) is retrieved and set to the `cartId` variable.</span></span> <span data-ttu-id="cc547-276">然後,調用`MigrateCart`該方法,將登錄`cartId`使用者和登錄使用者的名稱傳遞給此方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-276">Then, the `MigrateCart` method is called, passing both the `cartId` and the name of the logged-in user to this method.</span></span> <span data-ttu-id="cc547-277">遷移購物車時,用於標識匿名購物車的 GUID 將替換為使用者名。</span><span class="sxs-lookup"><span data-stu-id="cc547-277">When the shopping cart is migrated, the GUID used to identify the anonymous shopping cart is replaced with the user name.</span></span>

<span data-ttu-id="cc547-278">除了修改*Login.aspx.cs*代碼背後的檔以在使用者登錄時遷移購物車外,還必須修改*Register.aspx.cs代碼背後的檔*,以在使用者創建新帳戶並登錄時遷移購物車。</span><span class="sxs-lookup"><span data-stu-id="cc547-278">In addition to modifying the *Login.aspx.cs* code-behind file to migrate the shopping cart when the user logs in, you must also modify the *Register.aspx.cs code-behind file* to migrate the shopping cart when the user creates a new account and logs in.</span></span>

1. <span data-ttu-id="cc547-279">在 *「帳戶」* 資料夾中,打開名為*Register.aspx.cs*的碼隱藏檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-279">In the *Account* folder, open the code-behind file named *Register.aspx.cs*.</span></span>
2. <span data-ttu-id="cc547-280">以將代碼以黃色表示修改代碼後檔,以便它如下所示:</span><span class="sxs-lookup"><span data-stu-id="cc547-280">Modify the code-behind file by including the code in yellow, so that it appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. <span data-ttu-id="cc547-281">保存*Register.aspx.cs*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-281">Save the *Register.aspx.cs* file.</span></span> <span data-ttu-id="cc547-282">再次忽略有關方法的警告`MigrateCart`。</span><span class="sxs-lookup"><span data-stu-id="cc547-282">Once again, ignore the warning about the `MigrateCart` method.</span></span>

<span data-ttu-id="cc547-283">請注意,在`CreateUser_Click`事件處理程式中使用的代碼與方法中使用的`LogIn`代碼非常相似。</span><span class="sxs-lookup"><span data-stu-id="cc547-283">Notice that the code you used in the `CreateUser_Click` event handler is very similar to the code you used in the `LogIn` method.</span></span> <span data-ttu-id="cc547-284">當使用者註冊或登入網站時,將呼叫該方法`MigrateCart`。</span><span class="sxs-lookup"><span data-stu-id="cc547-284">When the user registers or logs in to the site, a call to the `MigrateCart` method will be made.</span></span>

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="cc547-285">遷移購物車</span><span class="sxs-lookup"><span data-stu-id="cc547-285">Migrating the Shopping Cart</span></span>

<span data-ttu-id="cc547-286">現在,您已經更新了登錄和註冊過程,您可以添加代碼以使用方法`MigrateCart`遷移購物車。</span><span class="sxs-lookup"><span data-stu-id="cc547-286">Now that you have the log-in and registration process updated, you can add the code to migrate the shopping cart using the `MigrateCart` method.</span></span>

1. <span data-ttu-id="cc547-287">在**解決方案資源管理員**中,尋找*邏輯*資料夾並打開*ShoppingCartActions.cs*類檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-287">In **Solution Explorer**, find the *Logic* folder and open the *ShoppingCartActions.cs* class file.</span></span>
2. <span data-ttu-id="cc547-288">將以黃色突顯的代碼加入*到 ShoppingCartActions.cs*檔案中的現有代碼,以便*ShoppingCartActions.cs*檔案中的程式碼如下所示:</span><span class="sxs-lookup"><span data-stu-id="cc547-288">Add the code highlighted in yellow to the existing code in the *ShoppingCartActions.cs* file, so that the code in the *ShoppingCartActions.cs* file appears as follows:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

<span data-ttu-id="cc547-289">該方法`MigrateCart`使用現有的購物車 Id 查找使用者的購物車。</span><span class="sxs-lookup"><span data-stu-id="cc547-289">The `MigrateCart` method uses the existing cartId to find the shopping cart of the user.</span></span> <span data-ttu-id="cc547-290">接下來,代碼迴圈遍歷所有購物車專案,`CartId`並將屬性(`CartItem`由架構指定)替換為登錄的使用者名。</span><span class="sxs-lookup"><span data-stu-id="cc547-290">Next, the code loops through all the shopping cart items and replaces the `CartId` property (as specified by the `CartItem` schema) with the logged-in user name.</span></span>

### <a name="updating-the-database-connection"></a><span data-ttu-id="cc547-291">更新資料庫連線</span><span class="sxs-lookup"><span data-stu-id="cc547-291">Updating the Database Connection</span></span>

<span data-ttu-id="cc547-292">如果您使用**預建**建的 Wingtip Toys 範例應用程式遵循本教學,則必須重新建立預設成員資格資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc547-292">If you are following this tutorial using the **prebuilt** Wingtip Toys sample application, you must recreate the default membership database.</span></span> <span data-ttu-id="cc547-293">通過修改預設連接字串,將在下次應用程式運行時創建成員資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc547-293">By modifying the default connection string, the membership database will be created the next time the application runs.</span></span>

1. <span data-ttu-id="cc547-294">開啟專案根目錄的*Web.config*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-294">Open the *Web.config* file at the root of the project.</span></span>
2. <span data-ttu-id="cc547-295">更新預設連接字串,使其如下所示:</span><span class="sxs-lookup"><span data-stu-id="cc547-295">Update the default connection string so that it appears as follows:</span></span>   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a><span data-ttu-id="cc547-296">整合貝寶</span><span class="sxs-lookup"><span data-stu-id="cc547-296">Integrating PayPal</span></span>

<span data-ttu-id="cc547-297">PayPal 是一個基於 Web 的計費平臺,接受在線商家的付款。</span><span class="sxs-lookup"><span data-stu-id="cc547-297">PayPal is a web-based billing platform that accepts payments by online merchants.</span></span> <span data-ttu-id="cc547-298">本教程接下來將介紹如何將 PayPal 的快速結帳功能集成到您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="cc547-298">This tutorial next explains how to integrate PayPal's Express Checkout functionality into your application.</span></span> <span data-ttu-id="cc547-299">快速結帳允許您的客戶使用 PayPal 支付已添加到購物車中的商品。</span><span class="sxs-lookup"><span data-stu-id="cc547-299">Express Checkout allows your customers to use PayPal to pay for the items they have added to their shopping cart.</span></span>

### <a name="create-paypal-test-accounts"></a><span data-ttu-id="cc547-300">建立貝寶測試帳戶</span><span class="sxs-lookup"><span data-stu-id="cc547-300">Create PayPal Test Accounts</span></span>

<span data-ttu-id="cc547-301">要使用 PayPal 測試環境,必須創建並驗證開發人員測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-301">To use the PayPal testing environment, you must create and verify a developer test account.</span></span> <span data-ttu-id="cc547-302">您將使用開發人員測試帳戶創建買方測試帳戶和賣方測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-302">You will use the developer test account to create a buyer test account and a seller test account.</span></span> <span data-ttu-id="cc547-303">開發人員測試帳戶認證使用者將允許翼尖玩具範例應用程式存取 PayPal 測試環境。</span><span class="sxs-lookup"><span data-stu-id="cc547-303">The developer test account credentials also will allow the Wingtip Toys sample application to access the PayPal testing environment.</span></span>

1. <span data-ttu-id="cc547-304">在瀏覽器中,導航到 PayPal 開發人員測試網站:</span><span class="sxs-lookup"><span data-stu-id="cc547-304">In a browser, navigate to the PayPal developer testing site:</span></span>   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. <span data-ttu-id="cc547-305">如果您沒有 PayPal 開發者帳戶,請通過單擊 **「註冊」** 並按照註冊步驟創建新帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-305">If you don't have a PayPal developer account, create a new account by clicking **Sign Up**and following the sign up steps.</span></span> <span data-ttu-id="cc547-306">如果您有現有的 PayPal 開發者帳戶,請通過單擊「**登錄**」 登錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-306">If you have an existing PayPal developer account, sign in by clicking **Log In**.</span></span> <span data-ttu-id="cc547-307">您將需要您的PayPal開發者帳戶來測試翼尖玩具範例應用程式稍後在本教程。</span><span class="sxs-lookup"><span data-stu-id="cc547-307">You will need your PayPal developer account to test the Wingtip Toys sample application later in this tutorial.</span></span>
3. <span data-ttu-id="cc547-308">如果您剛剛註冊了您的PayPal開發者帳戶,您可能需要使用PayPal驗證您的PayPal開發者帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-308">If you have just signed up for your PayPal developer account, you may need to verify your PayPal developer account with PayPal.</span></span> <span data-ttu-id="cc547-309">您可以按照 PayPal 發送到您的電子郵件帳戶的步驟驗證您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-309">You can verify your account by following the steps that PayPal sent to your email account.</span></span> <span data-ttu-id="cc547-310">驗證您的PayPal開發者帳戶後,請返回PayPal開發者測試網站。</span><span class="sxs-lookup"><span data-stu-id="cc547-310">Once you have verified your PayPal developer account, log back into the PayPal developer testing site.</span></span>
4. <span data-ttu-id="cc547-311">使用 PayPal 開發者帳戶登錄 PayPal 開發者網站後,如果您還沒有,則需要創建 PayPal 買家測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-311">After you are logged in to the PayPal developer site with your PayPal developer account you need to create a PayPal buyer test account if you don't already have one.</span></span> <span data-ttu-id="cc547-312">要創建買家測試帳戶,在 PayPal 網站上單擊 **「應用程式**」選項卡,然後單擊 **「沙箱帳戶**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-312">To create a buyer test account, on the PayPal site click the **Applications** tab and then click **Sandbox accounts**.</span></span>   
 <span data-ttu-id="cc547-313">將顯示沙**盒測試帳戶**頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-313">The **Sandbox test accounts** page is shown.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="cc547-314">PayPal 開發者網站已經提供了商家測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-314">The PayPal Developer site already provides a merchant test account.</span></span>

    ![使用 PayPal 結帳和付款 - 沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image15.png)
5. <span data-ttu-id="cc547-316">在沙箱測試帳戶頁上,按一下「**創建帳戶**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-316">On the Sandbox test accounts page, click **Create Account**.</span></span>
6. <span data-ttu-id="cc547-317">在 **「建立測試帳戶」** 頁上選擇買家測試帳戶電子郵件和您選擇的密碼。</span><span class="sxs-lookup"><span data-stu-id="cc547-317">On the **Create test account** page choose a buyer test account email and password of your choice.</span></span>   

    > [!NOTE] 
    > 
    > <span data-ttu-id="cc547-318">您將需要買家電子郵件地址和密碼來測試翼尖玩具示例應用程式在本教程的末尾。</span><span class="sxs-lookup"><span data-stu-id="cc547-318">You will need the buyer email addresses and password to test the Wingtip Toys sample application at the end of this tutorial.</span></span>

    ![使用 PayPal 結帳和付款 - 沙箱測試帳戶](checkout-and-payment-with-paypal/_static/image16.png)
7. <span data-ttu-id="cc547-320">通過按下 **「創建帳戶**」按鈕創建買方測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-320">Create the buyer test account by clicking the **Create Account** button.</span></span>  
 <span data-ttu-id="cc547-321">將顯示 **「沙箱測試帳戶」** 頁。</span><span class="sxs-lookup"><span data-stu-id="cc547-321">The **Sandbox Test accounts** page is displayed.</span></span> 

    ![使用貝寶結帳和付款 - 貝寶帳戶](checkout-and-payment-with-paypal/_static/image17.png)
8. <span data-ttu-id="cc547-323">在**沙箱測試帳戶**頁面上,單擊**主持人**電子郵件帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-323">On the **Sandbox test accounts** page, click the **facilitator** email account.</span></span>  
    <span data-ttu-id="cc547-324">將顯示**設定檔**和**通知**選項。</span><span class="sxs-lookup"><span data-stu-id="cc547-324">**Profile** and **Notification** options appear.</span></span>
9. <span data-ttu-id="cc547-325">選擇 **「設定檔」** 選項,然後單擊**API 認證的**以查看商家測試帳戶的 API 認證。</span><span class="sxs-lookup"><span data-stu-id="cc547-325">Select the **Profile** option, then click **API credentials** to view your API credentials for the merchant test account.</span></span>
10. <span data-ttu-id="cc547-326">將 TEST API 認證複製到記事本。</span><span class="sxs-lookup"><span data-stu-id="cc547-326">Copy the TEST API credentials to notepad.</span></span>

<span data-ttu-id="cc547-327">您需要顯示的經典測試 API 認證(使用者名稱、密碼和簽名)才能從 Wingtip Toys 範例應用程式向 PayPal 測試環境進行 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="cc547-327">You will need your displayed Classic TEST API credentials (Username, Password, and Signature) to make API calls from the Wingtip Toys sample application to the PayPal testing environment.</span></span> <span data-ttu-id="cc547-328">您將在下一步中添加憑據。</span><span class="sxs-lookup"><span data-stu-id="cc547-328">You will add the credentials in the next step.</span></span>

### <a name="add-paypal-class-and-api-credentials"></a><span data-ttu-id="cc547-329">新增貝寶類和 API 認證</span><span class="sxs-lookup"><span data-stu-id="cc547-329">Add PayPal Class and API Credentials</span></span>

<span data-ttu-id="cc547-330">您將將大多數 PayPal 代碼放入單個類中。</span><span class="sxs-lookup"><span data-stu-id="cc547-330">You will place the majority of the PayPal code into a single class.</span></span> <span data-ttu-id="cc547-331">此類包含用於與 PayPal 通信的方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-331">This class contains the methods used to communicate with PayPal.</span></span> <span data-ttu-id="cc547-332">此外,您將將您的 PayPal 認證到此類。</span><span class="sxs-lookup"><span data-stu-id="cc547-332">Also, you will add your PayPal credentials to this class.</span></span>

1. <span data-ttu-id="cc547-333">在 Visual Studio 中的 Wingtip 玩具範例應用程式中,右鍵單擊**邏輯**資料夾,然後選擇「**添加新** -&gt;**專案**」 。。</span><span class="sxs-lookup"><span data-stu-id="cc547-333">In the Wingtip Toys sample application within Visual Studio, right-click the **Logic** folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="cc547-334">[ **加入新項目** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="cc547-334">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="cc547-335">在左側 **「已安裝**」窗格中的 **「可視 C#」** 下,選擇 **「代碼**」 。。</span><span class="sxs-lookup"><span data-stu-id="cc547-335">Under **Visual C#** from the **Installed** pane on the left, select **Code**.</span></span>
3. <span data-ttu-id="cc547-336">從中間窗格中,選擇 **"類**"。</span><span class="sxs-lookup"><span data-stu-id="cc547-336">From the middle pane, select **Class**.</span></span> <span data-ttu-id="cc547-337">PayPalFunctions.cs命名此新**類。**</span><span class="sxs-lookup"><span data-stu-id="cc547-337">Name this new class **PayPalFunctions.cs**.</span></span>
4. <span data-ttu-id="cc547-338">按一下 **[新增]**。</span><span class="sxs-lookup"><span data-stu-id="cc547-338">Click **Add**.</span></span>  
   <span data-ttu-id="cc547-339">新的類文件顯示在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="cc547-339">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="cc547-340">使用下列程式碼來取代預設程式碼：</span><span class="sxs-lookup"><span data-stu-id="cc547-340">Replace the default code with the following code:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. <span data-ttu-id="cc547-341">添加您在本教程前面顯示的商家 API 認證(使用者名稱、密碼和簽名),以便您可以對 PayPal 測試環境進行函數調用。</span><span class="sxs-lookup"><span data-stu-id="cc547-341">Add the Merchant API credentials (Username, Password, and Signature) that you displayed earlier in this tutorial so that you can make function calls to the PayPal testing environment.</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="cc547-342">在此範例應用程式中,您只需向 C# 檔 (.cs) 添加認證。</span><span class="sxs-lookup"><span data-stu-id="cc547-342">In this sample application you are simply adding credentials to a C# file (.cs).</span></span> <span data-ttu-id="cc547-343">但是,在實施的解決方案中,應考慮在配置檔中加密憑據。</span><span class="sxs-lookup"><span data-stu-id="cc547-343">However, in a implemented solution, you should consider encrypting your credentials in a configuration file.</span></span>

<span data-ttu-id="cc547-344">NVPAPICaller 類包含大多數 PayPal 功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-344">The NVPAPICaller class contains the majority of the PayPal functionality.</span></span> <span data-ttu-id="cc547-345">類中的代碼提供了從 PayPal 測試環境進行測試購買所需的方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-345">The code in the class provides the methods needed to make a test purchase from the PayPal testing environment.</span></span> <span data-ttu-id="cc547-346">以下三個 PayPal 功能用於購買:</span><span class="sxs-lookup"><span data-stu-id="cc547-346">The following three PayPal functions are used to make purchases:</span></span>

- <span data-ttu-id="cc547-347">`SetExpressCheckout` 函式</span><span class="sxs-lookup"><span data-stu-id="cc547-347">`SetExpressCheckout` function</span></span>
- <span data-ttu-id="cc547-348">`GetExpressCheckoutDetails` 函式</span><span class="sxs-lookup"><span data-stu-id="cc547-348">`GetExpressCheckoutDetails` function</span></span>
- <span data-ttu-id="cc547-349">`DoExpressCheckoutPayment` 函式</span><span class="sxs-lookup"><span data-stu-id="cc547-349">`DoExpressCheckoutPayment` function</span></span>

<span data-ttu-id="cc547-350">該方法`ShortcutExpressCheckout`從購物車收集測試購買資訊和產品詳細資訊,並調`SetExpressCheckout`用 PayPal 功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-350">The `ShortcutExpressCheckout` method collects the test purchase information and product details from the shopping cart and calls the `SetExpressCheckout` PayPal function.</span></span> <span data-ttu-id="cc547-351">該方法`GetCheckoutDetails`確認購買詳細資訊,並在進行`GetExpressCheckoutDetails`測試 購買之前調用 PayPal 功能。</span><span class="sxs-lookup"><span data-stu-id="cc547-351">The `GetCheckoutDetails` method confirms purchase details and calls the `GetExpressCheckoutDetails` PayPal function before making the test purchase.</span></span> <span data-ttu-id="cc547-352">該方法`DoCheckoutPayment`通過調用 PayPal 函數完成從測試環境`DoExpressCheckoutPayment`中購買的 測試。</span><span class="sxs-lookup"><span data-stu-id="cc547-352">The `DoCheckoutPayment` method completes the test purchase from the testing environment by calling the `DoExpressCheckoutPayment` PayPal function.</span></span> <span data-ttu-id="cc547-353">其餘代碼支援 PayPal 方法和進程,例如編碼字串、解碼字串、處理陣列和確定認證。</span><span class="sxs-lookup"><span data-stu-id="cc547-353">The remaining code supports the PayPal methods and process, such as encoding strings, decoding strings, processing arrays, and determining credentials.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc547-354">PayPal允許您根據[PayPal 的API規範](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)包括可選的購買詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-354">PayPal allows you to include optional purchase details based on [PayPal's API specification](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout).</span></span> <span data-ttu-id="cc547-355">通過延伸 Wingtip Toys 範例應用程式中的代碼,您可以包括本地化詳細資訊、產品描述、稅金、客戶服務編號以及許多其他可選欄位。</span><span class="sxs-lookup"><span data-stu-id="cc547-355">By extending the code in the Wingtip Toys sample application, you can include localization details, product descriptions, tax, a customer service number, as well as many other optional fields.</span></span>

<span data-ttu-id="cc547-356">請注意,**在快捷方式 ExpressCheckout**方法中指定的傳回和取消 URL 使用埠號。</span><span class="sxs-lookup"><span data-stu-id="cc547-356">Notice that the return and cancel URLs that are specified in the **ShortcutExpressCheckout** method use a port number.</span></span>

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

<span data-ttu-id="cc547-357">當可視化 Web 開發人員使用 SSL 執行 Web 專案時,埠 44300 通常用於 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc547-357">When Visual Web Developer runs a web project using SSL, commonly the port 44300 is used for the web server.</span></span> <span data-ttu-id="cc547-358">如上所述,埠號為 44300。</span><span class="sxs-lookup"><span data-stu-id="cc547-358">As shown above, the port number is 44300.</span></span> <span data-ttu-id="cc547-359">運行應用程式時,可以看到不同的埠號。</span><span class="sxs-lookup"><span data-stu-id="cc547-359">When you run the application, you could see a different port number.</span></span> <span data-ttu-id="cc547-360">您的埠號需要在代碼中正確設置,以便您可以在本教程末尾成功運行 Wingtip Toys 示例應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-360">Your port number needs to be correctly set in the code so that you can successful run the Wingtip Toys sample application at the end of this tutorial.</span></span> <span data-ttu-id="cc547-361">本教程的下一部分將介紹如何檢索本地主機埠號並更新 PayPal 類。</span><span class="sxs-lookup"><span data-stu-id="cc547-361">The next section of this tutorial explains how to retrieve the local host port number and update the PayPal class.</span></span>

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a><span data-ttu-id="cc547-362">更新 PayPal 類別的本地主機連接埠號</span><span class="sxs-lookup"><span data-stu-id="cc547-362">Update the LocalHost Port Number in the PayPal Class</span></span>

<span data-ttu-id="cc547-363">翼尖玩具樣品應用程式購買產品通過導航到PayPal測試網站,並返回到您的本地實例的Wingtip玩具樣品應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-363">The Wingtip Toys sample application purchases products by navigating to the PayPal testing site and returning to your local instance of the Wingtip Toys sample application.</span></span> <span data-ttu-id="cc547-364">為了使 PayPal 傳回到正確的 URL,您需要在上面提到的 PayPal 代碼中指定本機執行的範例應用程式的連接埠號。</span><span class="sxs-lookup"><span data-stu-id="cc547-364">In order to have PayPal return to the correct URL, you need to specify the port number of the locally running sample application in the PayPal code mentioned above.</span></span>

1. <span data-ttu-id="cc547-365">右鍵按下**解決方案資源管理員**中的項目名稱 (**WingtipToys)** 並選擇**屬性**。</span><span class="sxs-lookup"><span data-stu-id="cc547-365">Right-click the project name (**WingtipToys**) in **Solution Explorer** and select **Properties**.</span></span>
2. <span data-ttu-id="cc547-366">在左列中,選擇 **「Web」** 選項卡。</span><span class="sxs-lookup"><span data-stu-id="cc547-366">In the left column, select the **Web** tab.</span></span>
3. <span data-ttu-id="cc547-367">從 **「專案 Url」** 框中檢索埠號。</span><span class="sxs-lookup"><span data-stu-id="cc547-367">Retrieve the port number from the **Project Url** box.</span></span>
4. <span data-ttu-id="cc547-368">如果需要,請更新*PayPalFunctions.cs*檔案`cancelURL`中的 PayPal 類別`NVPAPICaller`( ) 中的`returnURL`與, 以使用 Web 應用程式的連接埠號:</span><span class="sxs-lookup"><span data-stu-id="cc547-368">If needed, update the `returnURL` and `cancelURL` in the PayPal class (`NVPAPICaller`) in the *PayPalFunctions.cs* file to use the port number of your web application:</span></span>   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

<span data-ttu-id="cc547-369">現在,您添加的代碼將與本地 Web 應用程式的預期連接埠匹配。</span><span class="sxs-lookup"><span data-stu-id="cc547-369">Now the code that you added will match the expected port for your local Web application.</span></span> <span data-ttu-id="cc547-370">PayPal 將能夠返回到您本地電腦上的正確 URL。</span><span class="sxs-lookup"><span data-stu-id="cc547-370">PayPal will be able to return to the correct URL on your local machine.</span></span>

### <a name="add-the-paypal-checkout-button"></a><span data-ttu-id="cc547-371">新增貝寶結帳按鈕</span><span class="sxs-lookup"><span data-stu-id="cc547-371">Add the PayPal Checkout Button</span></span>

<span data-ttu-id="cc547-372">現在,主要 PayPal 函數已添加到範例應用程式中,您可以開始添加調用這些函數所需的標記和代碼。</span><span class="sxs-lookup"><span data-stu-id="cc547-372">Now that the primary PayPal functions have been added to the sample application, you can begin adding the markup and code needed to call these functions.</span></span> <span data-ttu-id="cc547-373">首先,您必須添加使用者將在購物車頁面上看到的結帳按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-373">First, you must add the checkout button that the user will see on the shopping cart page.</span></span>

1. <span data-ttu-id="cc547-374">打開*購物車.aspx*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-374">Open the *ShoppingCart.aspx* file.</span></span>
2. <span data-ttu-id="cc547-375">捲動到檔案底部並找到`<!--Checkout Placeholder -->`註解。</span><span class="sxs-lookup"><span data-stu-id="cc547-375">Scroll to the bottom of the file and find the `<!--Checkout Placeholder -->` comment.</span></span>
3. <span data-ttu-id="cc547-376">將註釋取代為`ImageButton`控制項,以便按照以下的標記:</span><span class="sxs-lookup"><span data-stu-id="cc547-376">Replace the comment with an `ImageButton` control so that the mark up is replaced as follows:</span></span>  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. <span data-ttu-id="cc547-377">在*ShoppingCart.aspx.cs*檔案中`UpdateBtn_Click`,在檔案末尾的事件處理程式之後`CheckOutBtn_Click`,新增事件處理程式:</span><span class="sxs-lookup"><span data-stu-id="cc547-377">In the *ShoppingCart.aspx.cs* file, after the `UpdateBtn_Click` event handler near the end of the file, add the `CheckOutBtn_Click` event handler:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. <span data-ttu-id="cc547-378">此外,在*ShoppingCart.aspx.cs*檔案中,添加`CheckoutBtn`對的引用,以便引用新的圖像按鈕如下:</span><span class="sxs-lookup"><span data-stu-id="cc547-378">Also in the *ShoppingCart.aspx.cs* file, add a reference to the `CheckoutBtn`, so that the new image button is referenced as follows:</span></span>  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. <span data-ttu-id="cc547-379">將更改保存到*ShoppingCart.aspx*檔和*ShoppingCart.aspx.cs*檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-379">Save your changes to both the *ShoppingCart.aspx* file and the *ShoppingCart.aspx.cs* file.</span></span>
7. <span data-ttu-id="cc547-380">從選單中,選擇**除錯**-&gt;**建構翼尖玩具**。</span><span class="sxs-lookup"><span data-stu-id="cc547-380">From the menu, select **Debug**-&gt;**Build WingtipToys**.</span></span>  
   <span data-ttu-id="cc547-381">該專案將使用新添加的**ImageButton**控制件進行重建。</span><span class="sxs-lookup"><span data-stu-id="cc547-381">The project will be rebuilt with the newly added **ImageButton** control.</span></span>

### <a name="send-purchase-details-to-paypal"></a><span data-ttu-id="cc547-382">向貝寶傳送購買詳情</span><span class="sxs-lookup"><span data-stu-id="cc547-382">Send Purchase Details to PayPal</span></span>

<span data-ttu-id="cc547-383">當使用者單擊購物車頁面上的 **「結帳**」按鈕 *(ShoppingCart.aspx)* 時,他們將開始購買過程。</span><span class="sxs-lookup"><span data-stu-id="cc547-383">When the user clicks the **Checkout** button on the shopping cart page (*ShoppingCart.aspx*), they'll begin the purchase process.</span></span> <span data-ttu-id="cc547-384">以下代碼調用購買產品所需的第一個 PayPal 函數。</span><span class="sxs-lookup"><span data-stu-id="cc547-384">The following code calls the first PayPal function needed to purchase products.</span></span>

1. <span data-ttu-id="cc547-385">從*簽出*資料夾中,打開名為*CheckoutStart.aspx.cs*的代碼隱藏檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-385">From the *Checkout* folder, open the code-behind file named *CheckoutStart.aspx.cs*.</span></span>   
   <span data-ttu-id="cc547-386">請務必打開代碼背後的檔。</span><span class="sxs-lookup"><span data-stu-id="cc547-386">Be sure to open the code-behind file.</span></span>
2. <span data-ttu-id="cc547-387">將現有的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="cc547-387">Replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

<span data-ttu-id="cc547-388">當應用程式的使用者按一下購物車頁面上的 **「簽出**」按鈕時,瀏覽器將導航到 *「結帳開始」.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-388">When the user of the application clicks the **Checkout** button on the shopping cart page, the browser will navigate to the *CheckoutStart.aspx* page.</span></span> <span data-ttu-id="cc547-389">當*簽出Start.aspx*頁面載入`ShortcutExpressCheckout`時, 將調用該方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-389">When the *CheckoutStart.aspx* page loads, the `ShortcutExpressCheckout` method is called.</span></span> <span data-ttu-id="cc547-390">此時,使用者將轉移到 PayPal 測試網站。</span><span class="sxs-lookup"><span data-stu-id="cc547-390">At this point, the user is transferred to the PayPal testing web site.</span></span> <span data-ttu-id="cc547-391">在PayPal網站上,使用者輸入其PayPal憑據,查看購買詳情,接受PayPal協定,並返回到`ShortcutExpressCheckout`方法完成端的 Wingtip 玩具示例應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-391">On the PayPal site, the user enters their PayPal credentials, reviews the purchase details, accepts the PayPal agreement and returns to the Wingtip Toys sample application where the `ShortcutExpressCheckout` method completes.</span></span> <span data-ttu-id="cc547-392">方法完成後,它將使用者重定向到`ShortcutExpressCheckout`方法中指定的*CheckoutReview.aspx*頁面。 `ShortcutExpressCheckout`</span><span class="sxs-lookup"><span data-stu-id="cc547-392">When the `ShortcutExpressCheckout` method is complete, it will redirect the user to the *CheckoutReview.aspx* page specified in the `ShortcutExpressCheckout` method.</span></span> <span data-ttu-id="cc547-393">這允許使用者從翼尖玩具示例應用程式中查看訂單詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-393">This allows the user to review the order details from within the Wingtip Toys sample application.</span></span>

### <a name="review-order-details"></a><span data-ttu-id="cc547-394">檢視訂單詳細資訊</span><span class="sxs-lookup"><span data-stu-id="cc547-394">Review Order Details</span></span>

<span data-ttu-id="cc547-395">從PayPal返回後,Wingtip玩具示例應用程式的*結帳審查.aspx*頁面將顯示訂單詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-395">After returning from PayPal, the *CheckoutReview.aspx* page of the Wingtip Toys sample application displays the order details.</span></span> <span data-ttu-id="cc547-396">此頁面允許使用者在購買產品之前查看訂單詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-396">This page allows the user to review the order details before purchasing the products.</span></span> <span data-ttu-id="cc547-397">"*結帳審核.aspx"* 頁必須建立如下:</span><span class="sxs-lookup"><span data-stu-id="cc547-397">The *CheckoutReview.aspx* page must be created as follows:</span></span>

1. <span data-ttu-id="cc547-398">在 *「簽出」* 資料夾中,打開名為 *「簽出Review.aspx」的*頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-398">In the *Checkout* folder, open the page named *CheckoutReview.aspx*.</span></span>
2. <span data-ttu-id="cc547-399">將現有標記取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-399">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. <span data-ttu-id="cc547-400">開啟名為*CheckoutReview.aspx.cs*的代碼後面頁,並將現有代碼取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-400">Open the code-behind page named *CheckoutReview.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

<span data-ttu-id="cc547-401">**"詳細資訊視圖"** 控制件用於顯示從 PayPal 返回的訂單詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-401">The **DetailsView** control is used to display the order details that have been returned from PayPal.</span></span> <span data-ttu-id="cc547-402">此外,上述代碼將訂單詳細資訊作為`OrderDetail`物件保存到 Wingtip Toys 資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc547-402">Also, the above code saves the order details to the Wingtip Toys database as an `OrderDetail` object.</span></span> <span data-ttu-id="cc547-403">當使用者按下「**完成訂單」** 按鈕時,他們將重定向到 *「結帳完成.aspx」* 頁。</span><span class="sxs-lookup"><span data-stu-id="cc547-403">When the user clicks on the **Complete Order** button, they are redirected to the *CheckoutComplete.aspx* page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc547-404">**提示**</span><span class="sxs-lookup"><span data-stu-id="cc547-404">**Tip**</span></span>
> 
> <span data-ttu-id="cc547-405">在 *"結帳Review.aspx"* 頁的標記中,請`<ItemStyle>`注意該 標記用於更改頁面底部附近的 **「詳細資訊查看」** 控制件中的項樣式。</span><span class="sxs-lookup"><span data-stu-id="cc547-405">In the markup of the *CheckoutReview.aspx* page, notice that the `<ItemStyle>` tag is used to change the style of the items within the **DetailsView** control near the bottom of the page.</span></span> <span data-ttu-id="cc547-406">通過在 **「設計檢視**」中查看頁面(透過在 Visual Studio 的左下角選擇 **「設計**」),然後選擇 **「詳細資訊檢視」** 控制項,然後選擇**智慧標記**(控制器右上角的箭頭圖示),您將能夠看到 **「詳細資訊查看任務**」 。。</span><span class="sxs-lookup"><span data-stu-id="cc547-406">By viewing the page in **Design View** (by selecting **Design** at the lower left corner of Visual Studio), then selecting the **DetailsView** control, and selecting the **Smart Tag** (the arrow icon at the top right of the control), you will be able to see the **DetailsView Tasks**.</span></span>
> 
> ![使用 PayPal 結帳和付款 - 編輯欄位](checkout-and-payment-with-paypal/_static/image18.png)
> 
> <span data-ttu-id="cc547-408">通過選擇 **「編輯欄位**」,「**欄位」** 對話框將顯示。</span><span class="sxs-lookup"><span data-stu-id="cc547-408">By selecting **Edit Fields**, the **Fields** dialog box will appear.</span></span> <span data-ttu-id="cc547-409">在此對話框中,您可以輕鬆地控制 **「詳細資訊檢視」** 控制件的可視屬性,如**ItemStyle。**</span><span class="sxs-lookup"><span data-stu-id="cc547-409">In this dialog box you can easily control the visual properties, such as **ItemStyle**, of the **DetailsView** control.</span></span>
> 
> ![使用 PayPal 結帳和付款 - 欄位對話框](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a><span data-ttu-id="cc547-411">完成購買</span><span class="sxs-lookup"><span data-stu-id="cc547-411">Complete Purchase</span></span>

<span data-ttu-id="cc547-412">*結帳完成.aspx*頁面從 PayPal 進行購買。</span><span class="sxs-lookup"><span data-stu-id="cc547-412">*CheckoutComplete.aspx* page makes the purchase from PayPal.</span></span> <span data-ttu-id="cc547-413">如上所述,用戶必須先按下 **「完成訂單」** 按鈕,應用程式才能導航到 *「結帳完成.aspx」* 頁。</span><span class="sxs-lookup"><span data-stu-id="cc547-413">As mentioned above, the user must click on the **Complete Order** button before the application will navigate to the *CheckoutComplete.aspx* page.</span></span>

1. <span data-ttu-id="cc547-414">在 *「簽出」* 資料夾中,打開名為 *「簽出完成.aspx」* 的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-414">In the *Checkout* folder, open the page named *CheckoutComplete.aspx*.</span></span>
2. <span data-ttu-id="cc547-415">將現有標記取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-415">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. <span data-ttu-id="cc547-416">開啟名為*CheckoutComplete.aspx.cs*的代碼後面頁,並將現有代碼取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-416">Open the code-behind page named *CheckoutComplete.aspx.cs* and replace the existing code with the following:</span></span>   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

<span data-ttu-id="cc547-417">載入*簽出完成.aspx*頁`DoCheckoutPayment`時, 將調用 該方法。</span><span class="sxs-lookup"><span data-stu-id="cc547-417">When the *CheckoutComplete.aspx* page is loaded, the `DoCheckoutPayment` method is called.</span></span> <span data-ttu-id="cc547-418">如前所述,`DoCheckoutPayment`該方法完成了從PayPal測試環境的購買。</span><span class="sxs-lookup"><span data-stu-id="cc547-418">As mentioned earlier, the `DoCheckoutPayment` method completes the purchase from the PayPal testing environment.</span></span> <span data-ttu-id="cc547-419">一旦PayPal完成訂單的購買,「*結帳完成.aspx」* 頁面向購買者顯示付款`ID`交易記錄 。</span><span class="sxs-lookup"><span data-stu-id="cc547-419">Once PayPal has completed the purchase of the order, the *CheckoutComplete.aspx* page displays a payment transaction `ID` to the purchaser.</span></span>

### <a name="handle-cancel-purchase"></a><span data-ttu-id="cc547-420">處理取消購買</span><span class="sxs-lookup"><span data-stu-id="cc547-420">Handle Cancel Purchase</span></span>

<span data-ttu-id="cc547-421">如果用戶決定取消購買,他們將被定向到 *「結帳取消.aspx」* 頁面,在那裡他們將看到他們的訂單已被取消。</span><span class="sxs-lookup"><span data-stu-id="cc547-421">If the user decides to cancel the purchase, they will be directed to the *CheckoutCancel.aspx* page where they will see that their order has been cancelled.</span></span>

1. <span data-ttu-id="cc547-422">在 *「簽出*」資料夾中打開名為 *「簽出取消取消.aspx」* 的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-422">Open the page named *CheckoutCancel.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="cc547-423">將現有標記取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-423">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a><span data-ttu-id="cc547-424">處理購買錯誤</span><span class="sxs-lookup"><span data-stu-id="cc547-424">Handle Purchase Errors</span></span>

<span data-ttu-id="cc547-425">購買過程中的錯誤將由 *「結帳錯誤.aspx」* 頁處理。</span><span class="sxs-lookup"><span data-stu-id="cc547-425">Errors during the purchase process will be handled by the *CheckoutError.aspx* page.</span></span> <span data-ttu-id="cc547-426">如果出現錯誤,"*結帳開始.aspx"* 頁、*結帳審核.aspx*頁和 *"結帳完成.aspx"* 頁的代碼將分別重定向到 *"結帳錯誤.aspx"* 頁。</span><span class="sxs-lookup"><span data-stu-id="cc547-426">The code-behind of the *CheckoutStart.aspx* page, the *CheckoutReview.aspx* page, and the *CheckoutComplete.aspx* page will each redirect to the *CheckoutError.aspx* page if an error occurs.</span></span>

1. <span data-ttu-id="cc547-427">在*簽出*資料夾中打開名為 *「簽出錯誤.aspx」* 的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-427">Open the page named *CheckoutError.aspx* in the *Checkout* folder.</span></span>
2. <span data-ttu-id="cc547-428">將現有標記取代為以下內容:</span><span class="sxs-lookup"><span data-stu-id="cc547-428">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

<span data-ttu-id="cc547-429">*簽出錯誤.aspx*頁面在結帳過程中發生錯誤時顯示錯誤詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cc547-429">The *CheckoutError.aspx* page is displayed with the error details when an error occurs during the checkout process.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="cc547-430">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="cc547-430">Running the Application</span></span>

<span data-ttu-id="cc547-431">運行應用程式以查看如何購買產品。</span><span class="sxs-lookup"><span data-stu-id="cc547-431">Run the application to see how to purchase products.</span></span> <span data-ttu-id="cc547-432">請注意,您將在 PayPal 測試環境中運行。</span><span class="sxs-lookup"><span data-stu-id="cc547-432">Note that you will be running in the PayPal testing environment.</span></span> <span data-ttu-id="cc547-433">沒有實際資金被兌換。</span><span class="sxs-lookup"><span data-stu-id="cc547-433">No actual money is being exchanged.</span></span>

1. <span data-ttu-id="cc547-434">請確保所有檔都保存在可視化工作室中。</span><span class="sxs-lookup"><span data-stu-id="cc547-434">Make sure all your files are saved in Visual Studio.</span></span>
2. <span data-ttu-id="cc547-435">開啟網頁瀏覽器並瀏[https://developer.paypal.com](https://developer.paypal.com/)覽到 。</span><span class="sxs-lookup"><span data-stu-id="cc547-435">Open a Web browser and navigate to [https://developer.paypal.com](https://developer.paypal.com/).</span></span>
3. <span data-ttu-id="cc547-436">使用您在本教程中之前創建的 PayPal 開發者帳戶登錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-436">Login with your PayPal developer account that you created earlier in this tutorial.</span></span>  
   <span data-ttu-id="cc547-437">對於 PayPal 的開發人員沙箱,您[https://developer.paypal.com](https://developer.paypal.com/)需要登錄 以測試快速結帳。</span><span class="sxs-lookup"><span data-stu-id="cc547-437">For PayPal's developer sandbox, you need to be logged in at [https://developer.paypal.com](https://developer.paypal.com/) to test express checkout.</span></span> <span data-ttu-id="cc547-438">這僅適用於貝寶的沙箱測試,不適用於PayPal的現場環境。</span><span class="sxs-lookup"><span data-stu-id="cc547-438">This only applies to PayPal's sandbox testing, not to PayPal's live environment.</span></span>
4. <span data-ttu-id="cc547-439">在視覺工作室中,按**F5**運行翼尖玩具示例應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc547-439">In Visual Studio, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="cc547-440">重建資料庫後,瀏覽器將打開並顯示*Default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="cc547-440">After the database rebuilds, the browser will open and show the *Default.aspx* page.</span></span>
5. <span data-ttu-id="cc547-441">通過選擇產品類別(如"汽車",然後單擊每個產品旁邊的 **「添加到購物車**」),將三種不同的產品添加到購物車中。</span><span class="sxs-lookup"><span data-stu-id="cc547-441">Add three different products to the shopping cart by selecting the product category, such as "Cars" and then clicking **Add to Cart** next to each product.</span></span>  
   <span data-ttu-id="cc547-442">購物車將顯示您選擇的產品。</span><span class="sxs-lookup"><span data-stu-id="cc547-442">The shopping cart will display the product you have selected.</span></span>
6. <span data-ttu-id="cc547-443">按下 **「貝寶**」按鈕進行結帳。</span><span class="sxs-lookup"><span data-stu-id="cc547-443">Click the **PayPal** button to checkout.</span></span> 

    ![使用PayPal結帳和付款 - 購物車](checkout-and-payment-with-paypal/_static/image20.png)

   <span data-ttu-id="cc547-445">簽出需要您擁有翼尖玩具範例應用程式的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-445">Checking out will require that you have a user account for the Wingtip Toys sample application.</span></span>
7. <span data-ttu-id="cc547-446">按一下頁面右側的**Google**連結,使用現有的gmail.com電子郵件帳戶登錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-446">Click the **Google** link on the right of the page to log in with an existing gmail.com email account.</span></span>  
   <span data-ttu-id="cc547-447">如果您沒有gmail.com帳戶,則可以在[www.gmail.com](https://www.gmail.com/)創建一個帳戶用於測試目的。</span><span class="sxs-lookup"><span data-stu-id="cc547-447">If you do not have a gmail.com account, you can create one for testing purposes at [www.gmail.com](https://www.gmail.com/).</span></span> <span data-ttu-id="cc547-448">您也可以通過按一下「註冊」使用標準本地帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-448">You can also use a standard local account by clicking "Register".</span></span> 

    ![使用 PayPal 結帳和付款 - 登入](checkout-and-payment-with-paypal/_static/image21.png)
8. <span data-ttu-id="cc547-450">使用 gmail 帳戶和密碼登錄。</span><span class="sxs-lookup"><span data-stu-id="cc547-450">Sign in with your gmail account and password.</span></span> 

    ![使用PayPal結帳和付款 - Gmail登錄](checkout-and-payment-with-paypal/_static/image22.png)
9. <span data-ttu-id="cc547-452">單擊**登錄**按鈕,使用翼尖玩具示例應用程式用戶名註冊您的 gmail 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc547-452">Click the **Log in** button to register your gmail account with your Wingtip Toys sample application user name.</span></span> 

    ![使用PayPal結帳和付款 - 註冊帳戶](checkout-and-payment-with-paypal/_static/image23.png)
10. <span data-ttu-id="cc547-454">在 PayPal 測試網站上,添加您在本教學中之前創建的**買家**電子郵件地址和密碼,然後按一**下 「登錄**」按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-454">On the PayPal test site, add your **buyer** email address and password that you created earlier in this tutorial, then click the **Log In** button.</span></span> 

    ![使用貝寶結帳和付款 - 貝寶登錄](checkout-and-payment-with-paypal/_static/image24.png)
11. <span data-ttu-id="cc547-456">同意 PayPal 政策,然後單擊 **「同意並繼續」** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-456">Agree to the PayPal policy and click the **Agree and Continue** button.</span></span>  
    <span data-ttu-id="cc547-457">請注意,此頁面僅在您首次使用此 PayPal 帳戶時顯示。</span><span class="sxs-lookup"><span data-stu-id="cc547-457">Note that this page is only displayed the first time you use this PayPal account.</span></span> <span data-ttu-id="cc547-458">再次注意,這是一個測試帳戶,沒有真正的錢交換。</span><span class="sxs-lookup"><span data-stu-id="cc547-458">Again note that this is a test account, no real money is exchanged.</span></span> 

    ![使用貝寶結帳和付款 - 貝寶政策](checkout-and-payment-with-paypal/_static/image25.png)
12. <span data-ttu-id="cc547-460">查看 PayPal 測試環境審核頁面上的訂單資訊,然後單擊"**繼續**"。</span><span class="sxs-lookup"><span data-stu-id="cc547-460">Review the order information on the PayPal testing environment review page and click **Continue**.</span></span> 

    ![使用 PayPal 結帳和付款 - 查看資訊](checkout-and-payment-with-paypal/_static/image26.png)
13. <span data-ttu-id="cc547-462">在 *「結帳審核.aspx」* 頁上,驗證訂單金額並查看生成的送貨位址。</span><span class="sxs-lookup"><span data-stu-id="cc547-462">On the *CheckoutReview.aspx* page, verify the order amount and view the generated shipping address.</span></span> <span data-ttu-id="cc547-463">然後,按一下完成**訂單**"按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc547-463">Then, click the **Complete Order** button.</span></span> 

    ![使用 PayPal 結帳和付款 - 訂單稽核](checkout-and-payment-with-paypal/_static/image27.png)
14. <span data-ttu-id="cc547-465">**"結帳完成.aspx"** 頁將顯示付款交易記錄 ID。</span><span class="sxs-lookup"><span data-stu-id="cc547-465">The **CheckoutComplete.aspx** page is displayed with a payment transaction ID.</span></span> 

    ![使用 PayPal 結帳和付款 - 結帳完成](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a><span data-ttu-id="cc547-467">檢視資料庫</span><span class="sxs-lookup"><span data-stu-id="cc547-467">Reviewing the Database</span></span>

<span data-ttu-id="cc547-468">通過在運行應用程式後查看 Wingtip Toys 範例應用程式資料庫中的更新數據,您可以看到應用程式已成功記錄產品的購買。</span><span class="sxs-lookup"><span data-stu-id="cc547-468">By reviewing the updated data in the Wingtip Toys sample application database after running the application, you can see that the application successfully recorded the purchase of the products.</span></span>

<span data-ttu-id="cc547-469">您可以使用**資料庫資源管理員**視窗(Visual Studio 中的**伺服器資源管理員**視窗)來檢查*Wingtiptoys.mdf*資料庫檔中的數據,就像本教學系列前面所做的那樣。</span><span class="sxs-lookup"><span data-stu-id="cc547-469">You can inspect the data contained in the *Wingtiptoys.mdf* database file by using the **Database Explorer** window (**Server Explorer** window in Visual Studio) as you did earlier in this tutorial series.</span></span>

1. <span data-ttu-id="cc547-470">如果瀏覽器視窗仍然打開,則關閉它。</span><span class="sxs-lookup"><span data-stu-id="cc547-470">Close the browser window if it is still open.</span></span>
2. <span data-ttu-id="cc547-471">在視覺化工作室中,選擇**解決方案資源管理員**頂部的 **「顯示所有檔**」圖示,以允許您展開**\_應用資料**資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc547-471">In Visual Studio, select the **Show All Files** icon at the top of **Solution Explorer** to allow you to expand the **App\_Data** folder.</span></span>
3. <span data-ttu-id="cc547-472">展開**應用\_數據**資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc547-472">Expand the **App\_Data** folder.</span></span>  
 <span data-ttu-id="cc547-473">您可能需要為資料夾選擇「**顯示所有檔案**」 圖示。</span><span class="sxs-lookup"><span data-stu-id="cc547-473">You may need to select the **Show All Files** icon for the folder.</span></span>
4. <span data-ttu-id="cc547-474">右鍵按*一下 Wingtiptoys.mdf*資料庫檔案,然後選擇 **「打開**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-474">Right-click the *Wingtiptoys.mdf* database file and select **Open**.</span></span>  
    <span data-ttu-id="cc547-475">將顯示**伺服器資源管理員**。</span><span class="sxs-lookup"><span data-stu-id="cc547-475">**Server Explorer** is displayed.</span></span>
5. <span data-ttu-id="cc547-476">展開 **[資料表]** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc547-476">Expand the **Tables** folder.</span></span>
6. <span data-ttu-id="cc547-477">右鍵按**下 「訂單**」表併選擇 **「顯示表數據**」。</span><span class="sxs-lookup"><span data-stu-id="cc547-477">Right-click the **Orders**table and select **Show Table Data**.</span></span>  
 <span data-ttu-id="cc547-478">將顯示 **「訂單**」表。</span><span class="sxs-lookup"><span data-stu-id="cc547-478">The **Orders** table is displayed.</span></span>
7. <span data-ttu-id="cc547-479">查看 **"付款交易ID"** 列以確認成功交易。</span><span class="sxs-lookup"><span data-stu-id="cc547-479">Review the **PaymentTransactionID** column to confirm successful transactions.</span></span> 

    ![使用 PayPal 結帳和付款 - 稽核資料庫](checkout-and-payment-with-paypal/_static/image29.png)
8. <span data-ttu-id="cc547-481">關閉**訂單**表視窗。</span><span class="sxs-lookup"><span data-stu-id="cc547-481">Close the **Orders** table window.</span></span>
9. <span data-ttu-id="cc547-482">在「伺服器資源管理器」中,右鍵按下 **「訂單詳細資訊**」表併選擇 **「顯示表數據**」 。</span><span class="sxs-lookup"><span data-stu-id="cc547-482">In the Server Explorer, right-click the **OrderDetails** table and select **Show Table Data**.</span></span>
10. <span data-ttu-id="cc547-483">查看 **「訂單詳細資訊**」表中`OrderId`的`Username`和值。</span><span class="sxs-lookup"><span data-stu-id="cc547-483">Review the `OrderId` and `Username` values in the **OrderDetails** table.</span></span> <span data-ttu-id="cc547-484">請注意,這些值與 **「訂單」** 表中`OrderId`包括`Username`的和值匹配。</span><span class="sxs-lookup"><span data-stu-id="cc547-484">Note that these values match the `OrderId` and `Username` values included in the **Orders** table.</span></span>
11. <span data-ttu-id="cc547-485">關閉 **「訂單詳細資訊**」表視窗。</span><span class="sxs-lookup"><span data-stu-id="cc547-485">Close the **OrderDetails** table window.</span></span>
12. <span data-ttu-id="cc547-486">右鍵按一下 Wingtip 玩具資料庫檔案 *(Wingtiptoys.mdf),* 然後選擇 **「關閉連接**」 。</span><span class="sxs-lookup"><span data-stu-id="cc547-486">Right-click the Wingtip Toys database file (*Wingtiptoys.mdf*) and select **Close Connection**.</span></span>
13. <span data-ttu-id="cc547-487">如果看不到**解決方案資源管理員**視窗,請按下**伺服器資源管理員**視窗底部**的解決方案資源管理員**,以再次顯示**解決方案資源管理員**。</span><span class="sxs-lookup"><span data-stu-id="cc547-487">If you do not see the **Solution Explorer** window, click **Solution Explorer** at the bottom of the **Server Explorer** window to show the **Solution Explorer** again.</span></span>

## <a name="summary"></a><span data-ttu-id="cc547-488">總結</span><span class="sxs-lookup"><span data-stu-id="cc547-488">Summary</span></span>

<span data-ttu-id="cc547-489">在本教程中,您添加了訂單和訂單詳細資訊架構,以跟蹤產品的購買情況。</span><span class="sxs-lookup"><span data-stu-id="cc547-489">In this tutorial you added order and order detail schemas to track the purchase of products.</span></span> <span data-ttu-id="cc547-490">您還可以將 PayPal 功能整合到翼尖玩具範例應用程式中。</span><span class="sxs-lookup"><span data-stu-id="cc547-490">You also integrated PayPal functionality into the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc547-491">其他資源</span><span class="sxs-lookup"><span data-stu-id="cc547-491">Additional Resources</span></span>

<span data-ttu-id="cc547-492">[ASP.NET 設定概述](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="cc547-492">[ASP.NET Configuration Overview](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="cc547-493">將具有成員資格、OAuth 和 SQL 資料庫的安全ASP.NET Web 窗體應用部署到 Azure 應用服務</span><span class="sxs-lookup"><span data-stu-id="cc547-493">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="cc547-494">微軟 Azure - 免費試用</span><span class="sxs-lookup"><span data-stu-id="cc547-494">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a><span data-ttu-id="cc547-495">免責聲明</span><span class="sxs-lookup"><span data-stu-id="cc547-495">Disclaimer</span></span>

<span data-ttu-id="cc547-496">本教程包含示例代碼。</span><span class="sxs-lookup"><span data-stu-id="cc547-496">This tutorial contains sample code.</span></span> <span data-ttu-id="cc547-497">此類示例代碼提供"有效",不提供任何形式的擔保。</span><span class="sxs-lookup"><span data-stu-id="cc547-497">Such sample code is provided "as is" without warranty of any kind.</span></span> <span data-ttu-id="cc547-498">因此,Microsoft 不保證範例代碼的準確性、完整性或品質。</span><span class="sxs-lookup"><span data-stu-id="cc547-498">Accordingly, Microsoft does not guarantee the accuracy, integrity, or quality of the sample code.</span></span> <span data-ttu-id="cc547-499">您同意自行承擔使用示例代碼的風險。</span><span class="sxs-lookup"><span data-stu-id="cc547-499">You agree to use the sample code at your own risk.</span></span> <span data-ttu-id="cc547-500">在任何情況下,Microsoft 均不對任何範例代碼、內容(包括但不限於任何範例代碼、內容中的任何錯誤或遺漏)或因使用任何示例代碼而造成的任何損失或損壞承擔任何責任。</span><span class="sxs-lookup"><span data-stu-id="cc547-500">Under no circumstances will Microsoft be liable to you in any way for any sample code, content, including but not limited to, any errors or omissions in any sample code, content, or any loss or damage of any kind incurred as a result of the use of any sample code.</span></span> <span data-ttu-id="cc547-501">特此通知您並同意對 Microsoft 的任何和所有損失、任何損失、傷害或損害索賠進行賠償、保存和保持無害,包括但不限於您發佈、傳輸、使用或依賴的材料引起的或由您所表達的意見引起的或產生的損失、傷害或損害。</span><span class="sxs-lookup"><span data-stu-id="cc547-501">You are hereby notified and do hereby agree to indemnify, save and hold Microsoft harmless from and against any and all loss, claims of loss, injury or damage of any kind including, without limitation, those occasioned by or arising from material that you post, transmit, use or rely on including, but not limited to, the views expressed therein.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc547-502">[前一個](shopping-cart.md)
> [下一個](membership-and-administration.md)</span><span class="sxs-lookup"><span data-stu-id="cc547-502">[Previous](shopping-cart.md)
[Next](membership-and-administration.md)</span></span>
