---
title: 如何：使用 Web Form 應用程式中的事件
description: 瞭解如何處理 ASP.NET Web Forms apps 中的按鈕點擊事件。
author: rick-anderson
ms.author: riande
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [ASP.NET], Web Forms
- Web Forms controls, and events
- event handlers [ASP.NET], Web Forms
- events [ASP.NET], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
ms.openlocfilehash: 2e1807fed7d03db5893e1767a7a3a0de81862e7f
ms.sourcegitcommit: db13f9477981daabd57b99a410ec34e31e8d6aae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674813"
---
# <a name="how-to-consume-events-in-a-web-forms-app"></a><span data-ttu-id="45a32-103">如何：使用 Web Form 應用程式中的事件</span><span class="sxs-lookup"><span data-stu-id="45a32-103">How to: Consume events in a Web Forms app</span></span>

<span data-ttu-id="45a32-104">ASP.NET Web Form 應用程式中的常見使用情況是使用控制項填入網頁，然後根據使用者所按的控制項，執行特定動作。</span><span class="sxs-lookup"><span data-stu-id="45a32-104">A common scenario in ASP.NET Web Forms applications is to populate a webpage with controls, and then perform a specific action based on which control the user clicks.</span></span> <span data-ttu-id="45a32-105">例如，當使用者在網頁中按一下 <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> 控制項時，控制項就會引發事件。</span><span class="sxs-lookup"><span data-stu-id="45a32-105">For example, a <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> control raises an event when the user clicks it in the webpage.</span></span> <span data-ttu-id="45a32-106">藉由處理事件，您的應用程式可以針對按一下按鈕執行適當的應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="45a32-106">By handling the event, your application can perform the appropriate application logic for that button click.</span></span>  
  
## <a name="handle-a-button-click-event-on-a-webpage"></a><span data-ttu-id="45a32-107">處理網頁上的按鈕點按事件</span><span class="sxs-lookup"><span data-stu-id="45a32-107">Handle a button-click event on a webpage</span></span>  
  
1. <span data-ttu-id="45a32-108">建立具有 <xref:System.Web.UI.WebControls.Button> 控制項的 ASP.NET Web Form 網頁 (網頁)，其中 `OnClick` 值設定為您將在下一個步驟中定義的方法名稱。</span><span class="sxs-lookup"><span data-stu-id="45a32-108">Create a ASP.NET Web Forms page (webpage) that has a <xref:System.Web.UI.WebControls.Button> control with the `OnClick` value set to the name of method that you will define in the next step.</span></span>  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. <span data-ttu-id="45a32-109">定義比對 <xref:System.Web.UI.WebControls.Button.Click> 事件委派簽章且採用您為 `OnClick` 值所定義名稱的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="45a32-109">Define an event handler that matches the <xref:System.Web.UI.WebControls.Button.Click> event delegate signature and that has the name you defined for the `OnClick` value.</span></span>  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     <span data-ttu-id="45a32-110"><xref:System.Web.UI.WebControls.Button.Click> 事件針對 <xref:System.EventHandler> 使用委派類型，並針對事件資料使用 <xref:System.EventArgs> 類別。</span><span class="sxs-lookup"><span data-stu-id="45a32-110">The <xref:System.Web.UI.WebControls.Button.Click> event uses the <xref:System.EventHandler> class for the delegate type and the <xref:System.EventArgs> class for the event data.</span></span> <span data-ttu-id="45a32-111">ASP.NET 網頁架構會自動產生程式碼，該程式碼會建立<xref:System.EventHandler> 執行個體，並將這個委派執行個體加入至 <xref:System.Web.UI.WebControls.Button.Click> 介面的 <xref:System.Web.UI.WebControls.Button> 事件。</span><span class="sxs-lookup"><span data-stu-id="45a32-111">The ASP.NET page framework automatically generates code that creates an instance of <xref:System.EventHandler> and adds this delegate instance to the <xref:System.Web.UI.WebControls.Button.Click> event of the <xref:System.Web.UI.WebControls.Button> instance.</span></span>  
  
3. <span data-ttu-id="45a32-112">在步驟 2 中定義的事件處理常式方法中加入程式碼，在事件發生時執行所需的任何動作。</span><span class="sxs-lookup"><span data-stu-id="45a32-112">In the event handler method that you defined in step 2, add code to perform any actions that are required when the event occurs.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="45a32-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="45a32-113">See also</span></span>

- [<span data-ttu-id="45a32-114">檢查與插入、更新和刪除相關聯的事件</span><span class="sxs-lookup"><span data-stu-id="45a32-114">Examine the Events Associated with Inserting, Updating, and Deleting</span></span>](data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
- [<span data-ttu-id="45a32-115">.NET 中的事件</span><span class="sxs-lookup"><span data-stu-id="45a32-115">Events in .NET</span></span>](/dotnet/standard/index.md)
