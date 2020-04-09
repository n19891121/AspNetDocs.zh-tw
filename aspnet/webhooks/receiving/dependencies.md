---
uid: webhooks/receiving/dependencies
title: ASP.NET WebHooks 接收器依賴項 |微軟文件
author: rick-anderson
description: ASP.NET WebHook 中的接收器依賴項和依賴項注入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: b50442b3d95512bc0db7583b93de3bbef2d4bb4a
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675205"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET WebHooks 接收器相依項

微軟ASP.NETWebHooks的設計考慮到了依賴注入。 使用依賴項注入引擎可以將系統中的大多數依賴項替換為替代實現。

有關接收器相依項清單,請參考[項目延伸](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs)。 如果未註冊依賴項,則使用預設實現。 有關預設實現的清單,請參閱[Receiver 服務](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs)。
