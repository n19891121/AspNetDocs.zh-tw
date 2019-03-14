---
ms.openlocfilehash: e5565381f44480e2531925717ee7815da92d1ff5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030035"
---
# <a name="update-the-generated-pages"></a>更新產生的頁面

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

剛開始使用此電影應用程式還不錯，但其呈現效果卻不理想。 我們不想看到時間 (下圖的 12:00:00 AM)，而且 **ReleaseDate** 應該是 **Release Date** (兩個分開的字)。

![在 Chrome 中開啟的電影應用程式顯示電影資料](../../tutorials/razor-pages/sql/_static/m55.png)

## <a name="update-the-generated-code"></a>更新產生的程式碼

開啟 *Models/Movie.cs* 檔案，然後新增下列程式碼中顯示的醒目提示行：

[!code-csharp[](code/Models/Movie.cs?highlight=2,11-12)]
