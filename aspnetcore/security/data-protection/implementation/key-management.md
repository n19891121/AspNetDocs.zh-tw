---
title: ASP.NET Core 中的金鑰管理
author: rick-anderson
description: 了解 ASP.NET Core 資料保護金鑰管理的 Api 實作詳細資料。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-management
ms.openlocfilehash: 431bdf2d3076c83279b78f327ddb647f69e6e584
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042575"
---
# <a name="key-management-in-aspnet-core"></a><span data-ttu-id="5b4b1-103">ASP.NET Core 中的金鑰管理</span><span class="sxs-lookup"><span data-stu-id="5b4b1-103">Key management in ASP.NET Core</span></span>

<a name="data-protection-implementation-key-management"></a>

<span data-ttu-id="5b4b1-104">資料保護系統會自動管理主要金鑰用來保護且取消保護承載的存留的期。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-104">The data protection system automatically manages the lifetime of master keys used to protect and unprotect payloads.</span></span> <span data-ttu-id="5b4b1-105">每個索引鍵可以存在於其中的四個階段：</span><span class="sxs-lookup"><span data-stu-id="5b4b1-105">Each key can exist in one of four stages:</span></span>

* <span data-ttu-id="5b4b1-106">建立索引鍵存在於金鑰環，但是尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-106">Created - the key exists in the key ring but has not yet been activated.</span></span> <span data-ttu-id="5b4b1-107">索引鍵不應該用於新的保護作業有足夠的時間經過之前，機碼有機會傳播到所有的機器會使用此金鑰環。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-107">The key shouldn't be used for new Protect operations until sufficient time has elapsed that the key has had a chance to propagate to all machines that are consuming this key ring.</span></span>

* <span data-ttu-id="5b4b1-108">使用中-索引鍵存在於金鑰環，並應用於所有新的保護作業。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-108">Active - the key exists in the key ring and should be used for all new Protect operations.</span></span>

* <span data-ttu-id="5b4b1-109">到期-機碼已執行其自然的存留期，並無法再用於新的保護作業。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-109">Expired - the key has run its natural lifetime and should no longer be used for new Protect operations.</span></span>

* <span data-ttu-id="5b4b1-110">撤銷-金鑰遭到入侵，且必須不適用於新的保護作業。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-110">Revoked - the key is compromised and must not be used for new Protect operations.</span></span>

<span data-ttu-id="5b4b1-111">建立、 使用中，且已過期的金鑰所有可用來取消保護傳入的裝載。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-111">Created, active, and expired keys may all be used to unprotect incoming payloads.</span></span> <span data-ttu-id="5b4b1-112">依預設已撤銷的金鑰不可取消保護內容，但應用程式開發人員可以[覆寫這個行為](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect)如有必要。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-112">Revoked keys by default may not be used to unprotect payloads, but the application developer can [override this behavior](xref:security/data-protection/consumer-apis/dangerous-unprotect#data-protection-consumer-apis-dangerous-unprotect) if necessary.</span></span>

>[!WARNING]
> <span data-ttu-id="5b4b1-113">開發人員可能會想要從金鑰環刪除金鑰，（例如，藉由從檔案系統中刪除對應的檔案）。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-113">The developer might be tempted to delete a key from the key ring (e.g., by deleting the corresponding file from the file system).</span></span> <span data-ttu-id="5b4b1-114">此時，金鑰所保護的所有資料都都會永久觸，並都沒有緊急的覆寫像是使用已撤銷的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-114">At that point, all data protected by the key is permanently undecipherable, and there's no emergency override like there's with revoked keys.</span></span> <span data-ttu-id="5b4b1-115">刪除索引鍵是真正破壞性的行為，因此資料保護系統會公開任何第一級的 API 執行此作業。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-115">Deleting a key is truly destructive behavior, and consequently the data protection system exposes no first-class API for performing this operation.</span></span>

## <a name="default-key-selection"></a><span data-ttu-id="5b4b1-116">預設索引鍵選取範圍</span><span class="sxs-lookup"><span data-stu-id="5b4b1-116">Default key selection</span></span>

<span data-ttu-id="5b4b1-117">當資料保護系統會讀取備份存放庫中的金鑰環時，它會嘗試找出金鑰環的 「 預設 」 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-117">When the data protection system reads the key ring from the backing repository, it will attempt to locate a "default" key from the key ring.</span></span> <span data-ttu-id="5b4b1-118">預設索引鍵用於新的保護作業。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-118">The default key is used for new Protect operations.</span></span>

<span data-ttu-id="5b4b1-119">一般的啟發學習法是資料保護系統會選擇具有最新的啟動日期做為預設索引鍵的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-119">The general heuristic is that the data protection system chooses the key with the most recent activation date as the default key.</span></span> <span data-ttu-id="5b4b1-120">（沒有以允許伺服器對伺服器的時鐘誤差小餘裕。）如果金鑰已過期或撤銷，且如果應用程式具有未停用自動金鑰產生，則會立即啟用每個產生新的金鑰[金鑰到期日和輪流](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration)下方的原則。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-120">(There's a small fudge factor to allow for server-to-server clock skew.) If the key is expired or revoked, and if the application has not disabled automatic key generation, then a new key will be generated with immediate activation per the [key expiration and rolling](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) policy below.</span></span>

<span data-ttu-id="5b4b1-121">資料保護系統的原因會立即產生新的金鑰，而不是正在回復到不同的索引鍵是新的金鑰產生應該視為隱含在新的金鑰之前所啟動的所有索引鍵的到期時間。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-121">The reason the data protection system generates a new key immediately rather than falling back to a different key is that new key generation should be treated as an implicit expiration of all keys that were activated prior to the new key.</span></span> <span data-ttu-id="5b4b1-122">新的金鑰可能已設定使用不同的演算法或比舊的金鑰，待用加密機制，而系統應該會偏好使用目前的設定透過回到的基本概念。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-122">The general idea is that new keys may have been configured with different algorithms or encryption-at-rest mechanisms than old keys, and the system should prefer the current configuration over falling back.</span></span>

<span data-ttu-id="5b4b1-123">沒有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-123">There's an exception.</span></span> <span data-ttu-id="5b4b1-124">如果應用程式開發人員[停用自動產生金鑰](xref:security/data-protection/configuration/overview#disableautomatickeygeneration)，則資料保護系統必須選擇做為預設索引鍵的項目。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-124">If the application developer has [disabled automatic key generation](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), then the data protection system must choose something as the default key.</span></span> <span data-ttu-id="5b4b1-125">在此後援的案例中，系統會選擇非撤銷鍵的最新的啟動日期，加上提供給有時間才能傳播至叢集中的其他電腦的索引鍵的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-125">In this fallback scenario, the system will choose the non-revoked key with the most recent activation date, with preference given to keys that have had time to propagate to other machines in the cluster.</span></span> <span data-ttu-id="5b4b1-126">後援系統可能會得到結果選擇過期的預設索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-126">The fallback system may end up choosing an expired default key as a result.</span></span> <span data-ttu-id="5b4b1-127">後援系統將永遠不會選擇做為預設索引鍵已撤銷的金鑰，而且如果 keyring 是空的或已撤銷的每個金鑰然後系統會產生在初始化時錯誤。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-127">The fallback system will never choose a revoked key as the default key, and if the key ring is empty or every key has been revoked then the system will produce an error upon initialization.</span></span>

<a name="data-protection-implementation-key-management-expiration"></a>

## <a name="key-expiration-and-rolling"></a><span data-ttu-id="5b4b1-128">金鑰到期日和正在復原</span><span class="sxs-lookup"><span data-stu-id="5b4b1-128">Key expiration and rolling</span></span>

<span data-ttu-id="5b4b1-129">建立金鑰時，它會自動提供 {now + 2 天} 啟用日和到期日的 {now + 90 天}。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-129">When a key is created, it's automatically given an activation date of { now + 2 days } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="5b4b1-130">2 天前的延遲啟動過程提供關鍵的時間才能傳播至整個系統。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-130">The 2-day delay before activation gives the key time to propagate through the system.</span></span> <span data-ttu-id="5b4b1-131">也就是說，它可讓其他應用程式指向備份存放區索引鍵觀察在其下一步 自動重新整理的間隔，因而能充分利用，當金鑰信號會變成作用中，它已傳播到所有的應用程式可能需要使用它的機會。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-131">That is, it allows other applications pointing at the backing store to observe the key at their next auto-refresh period, thus maximizing the chances that when the key ring does become active it has propagated to all applications that might need to use it.</span></span>

<span data-ttu-id="5b4b1-132">如果預設金鑰將在 2 天內過期，且金鑰環還沒有可使用在到期時的預設索引鍵的索引鍵，資料保護系統會自動保存金鑰環新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-132">If the default key will expire within 2 days and if the key ring doesn't already have a key that will be active upon expiration of the default key, then the data protection system will automatically persist a new key to the key ring.</span></span> <span data-ttu-id="5b4b1-133">這個新的金鑰具有 {預設的金鑰到期日} 啟用日和到期日的 {now + 90 天}。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-133">This new key has an activation date of { default key's expiration date } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="5b4b1-134">這可讓系統自動不中斷服務的定期輪替金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-134">This allows the system to automatically roll keys on a regular basis with no interruption of service.</span></span>

<span data-ttu-id="5b4b1-135">有可能在某些情況下立即啟用建立金鑰的位置。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-135">There might be circumstances where a key will be created with immediate activation.</span></span> <span data-ttu-id="5b4b1-136">其中一個範例就是當應用程式尚未執行的時間，而金鑰環中的所有金鑰已都過期。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-136">One example would be when the application hasn't run for a time and all keys in the key ring are expired.</span></span> <span data-ttu-id="5b4b1-137">當發生這種情況時，索引鍵有 {現在} 啟用日期，而不會正常 2 天的啟用延遲。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-137">When this happens, the key is given an activation date of { now } without the normal 2-day activation delay.</span></span>

<span data-ttu-id="5b4b1-138">預設金鑰存留期會是 90 天，但這是可設定，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-138">The default key lifetime is 90 days, though this is configurable as in the following example.</span></span>

```csharp
services.AddDataProtection()
       // use 14-day lifetime instead of 90-day lifetime
       .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
```

<span data-ttu-id="5b4b1-139">雖然明確呼叫，以系統管理員也可以變更預設全系統的`SetDefaultKeyLifetime`會覆寫任何全系統原則。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-139">An administrator can also change the default system-wide, though an explicit call to `SetDefaultKeyLifetime` will override any system-wide policy.</span></span> <span data-ttu-id="5b4b1-140">預設金鑰存留期不能少於 7 天。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-140">The default key lifetime cannot be shorter than 7 days.</span></span>

## <a name="automatic-key-ring-refresh"></a><span data-ttu-id="5b4b1-141">自動金鑰環重新整理</span><span class="sxs-lookup"><span data-stu-id="5b4b1-141">Automatic key ring refresh</span></span>

<span data-ttu-id="5b4b1-142">資料保護系統初始化時，它會讀取基礎儲存機制中的金鑰環，並快取在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-142">When the data protection system initializes, it reads the key ring from the underlying repository and caches it in memory.</span></span> <span data-ttu-id="5b4b1-143">此快取可讓您保護且取消保護作業繼續進行而不叫用的備份存放區。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-143">This cache allows Protect and Unprotect operations to proceed without hitting the backing store.</span></span> <span data-ttu-id="5b4b1-144">大約每隔 24 小時或目前的預設金鑰到期，視何者先時，系統會自動檢查變更的備份存放區。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-144">The system will automatically check the backing store for changes approximately every 24 hours or when the current default key expires, whichever comes first.</span></span>

>[!WARNING]
> <span data-ttu-id="5b4b1-145">（如果有的話） 開發人員應該很少需要直接使用管理 Api。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-145">Developers should very rarely (if ever) need to use the key management APIs directly.</span></span> <span data-ttu-id="5b4b1-146">資料保護系統會執行自動金鑰管理，如上面所述。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-146">The data protection system will perform automatic key management as described above.</span></span>

<span data-ttu-id="5b4b1-147">資料保護系統公開介面`IKeyManager`，可用來檢查及變更金鑰環。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-147">The data protection system exposes an interface `IKeyManager` that can be used to inspect and make changes to the key ring.</span></span> <span data-ttu-id="5b4b1-148">DI 系統提供的執行個體`IDataProtectionProvider`也可以提供的執行個體`IKeyManager`供您取用。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-148">The DI system that provided the instance of `IDataProtectionProvider` can also provide an instance of `IKeyManager` for your consumption.</span></span> <span data-ttu-id="5b4b1-149">或者，您可以提取`IKeyManager`直接從`IServiceProvider`如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-149">Alternatively, you can pull the `IKeyManager` straight from the `IServiceProvider` as in the example below.</span></span>

<span data-ttu-id="5b4b1-150">可修改 keyring （明確地建立新的金鑰，或執行撤銷） 的任何作業會導致無效的記憶體中快取。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-150">Any operation which modifies the key ring (creating a new key explicitly or performing a revocation) will invalidate the in-memory cache.</span></span> <span data-ttu-id="5b4b1-151">下次呼叫`Protect`或`Unprotect`會導致重新讀取金鑰環，並重新建立快取的資料保護系統。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-151">The next call to `Protect` or `Unprotect` will cause the data protection system to reread the key ring and recreate the cache.</span></span>

<span data-ttu-id="5b4b1-152">下列範例示範如何使用`IKeyManager`介面，以檢查及操作 keyring，包括撤銷現有的機碼和手動產生新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-152">The sample below demonstrates using the `IKeyManager` interface to inspect and manipulate the key ring, including revoking existing keys and generating a new key manually.</span></span>

[!code-csharp[](key-management/samples/key-management.cs)]

## <a name="key-storage"></a><span data-ttu-id="5b4b1-153">金鑰儲存</span><span class="sxs-lookup"><span data-stu-id="5b4b1-153">Key storage</span></span>

<span data-ttu-id="5b4b1-154">資料保護系統有啟發學習法，因此它會嘗試自動推斷適當金鑰的儲存位置和待用加密機制。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-154">The data protection system has a heuristic whereby it attempts to deduce an appropriate key storage location and encryption-at-rest mechanism automatically.</span></span> <span data-ttu-id="5b4b1-155">也可由應用程式開發人員設定金鑰持續性機制。</span><span class="sxs-lookup"><span data-stu-id="5b4b1-155">The key persistence mechanism is also configurable by the app developer.</span></span> <span data-ttu-id="5b4b1-156">下列文件將討論這些機制的內建實作：</span><span class="sxs-lookup"><span data-stu-id="5b4b1-156">The following documents discuss the in-box implementations of these mechanisms:</span></span>

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>
