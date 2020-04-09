---
uid: webhooks/diagnostics/debugging
title: ASP.NET WebHooks 調試 |微軟文件
author: rick-anderson
description: 如何調試ASP.NET WebHooks。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 2f1f8196478e7025a0467acb945d9ed36c8fd0ca
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675373"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET WebHooks 除錯

## <a name="debugging-in-azure"></a>在 Azure 中除錯

在 Azure 中執行時除錯 Web 應用程式,請參閱[使用 Visual Studio 在 Azure 應用服務中對 Web 應用進行故障排除教學](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="debugging-with-source-and-symbols"></a>使用來源與符號進行除錯

除了調試自己的代碼外,還可以直接調試到 Microsoft ASP.NET WebHooks,實際上還可以調試到所有 .NET。 無論您在本地調試還是遠端調試,這都有效。 首先,通過去**調試**,然後選擇**和設置**,配置 Visual Studio 以查找源和符號。 設定以下的選項:

![選項與設定](_static/SourceSymbols.png)

然後添加指向[symbolsource.org](http://symbolsource.org)的鏈接以下載源和符號。 跳到上面選單的 **「符號」** 選項卡,並將以下內容新增為符號位置:

```
http://srv.symbolsource.org/pdb/Public
```

此外,請確保緩存目錄具有短名稱;否則,檔名可能會太長,這將導致符號無法載入。 範例路徑是:

```
C:\SymCache
```

設定應如下所示:

![選項符號檔案位置範例](_static/SymSource.png)
