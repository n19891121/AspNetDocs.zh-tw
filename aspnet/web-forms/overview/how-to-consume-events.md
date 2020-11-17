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
# <a name="how-to-consume-events-in-a-web-forms-app"></a>如何：使用 Web Form 應用程式中的事件

ASP.NET Web Form 應用程式中的常見使用情況是使用控制項填入網頁，然後根據使用者所按的控制項，執行特定動作。 例如，當使用者在網頁中按一下 <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> 控制項時，控制項就會引發事件。 藉由處理事件，您的應用程式可以針對按一下按鈕執行適當的應用程式邏輯。  
  
## <a name="handle-a-button-click-event-on-a-webpage"></a>處理網頁上的按鈕點按事件  
  
1. 建立具有 <xref:System.Web.UI.WebControls.Button> 控制項的 ASP.NET Web Form 網頁 (網頁)，其中 `OnClick` 值設定為您將在下一個步驟中定義的方法名稱。  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. 定義比對 <xref:System.Web.UI.WebControls.Button.Click> 事件委派簽章且採用您為 `OnClick` 值所定義名稱的事件處理常式。  
  
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
  
     <xref:System.Web.UI.WebControls.Button.Click> 事件針對 <xref:System.EventHandler> 使用委派類型，並針對事件資料使用 <xref:System.EventArgs> 類別。 ASP.NET 網頁架構會自動產生程式碼，該程式碼會建立<xref:System.EventHandler> 執行個體，並將這個委派執行個體加入至 <xref:System.Web.UI.WebControls.Button.Click> 介面的 <xref:System.Web.UI.WebControls.Button> 事件。  
  
3. 在步驟 2 中定義的事件處理常式方法中加入程式碼，在事件發生時執行所需的任何動作。  
  
## <a name="see-also"></a>另請參閱

- [檢查與插入、更新和刪除相關聯的事件](data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
- [.NET 中的事件](/dotnet/standard/index.md)
