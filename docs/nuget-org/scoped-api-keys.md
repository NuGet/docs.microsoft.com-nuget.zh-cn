---
title: 范围内的 API 密钥
description: 控制用于推送包的 API 密钥
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426942"
---
# <a name="scoped-api-keys"></a><span data-ttu-id="9d09a-103">范围内的 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-103">Scoped API keys</span></span>

<span data-ttu-id="9d09a-104">为了使 NuGet 成为一个更安全的包分发环境，可以通过添加范围来控制 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-104">To make NuGet a more secure environment for package distribution, you can take control of the API keys by adding scopes.</span></span>

<span data-ttu-id="9d09a-105">借助向 API 密钥提供范围的功能可更好地控制 API。</span><span class="sxs-lookup"><span data-stu-id="9d09a-105">The ability to provide scope to your API keys give you better control on your APIs.</span></span> <span data-ttu-id="9d09a-106">你可以：</span><span class="sxs-lookup"><span data-stu-id="9d09a-106">You can:</span></span>

- <span data-ttu-id="9d09a-107">创建多个范围内的 API 密钥，可用于具有不同到期时间表的不同包。</span><span class="sxs-lookup"><span data-stu-id="9d09a-107">Create multiple scoped API keys that can be used for different packages with varying expiration timeframes.</span></span>
- <span data-ttu-id="9d09a-108">安全地获取 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-108">Obtain API keys securely.</span></span>
- <span data-ttu-id="9d09a-109">编辑现有 API 密钥以更改包适用性。</span><span class="sxs-lookup"><span data-stu-id="9d09a-109">Edit existing API keys to change package applicability.</span></span>
- <span data-ttu-id="9d09a-110">刷新或删除现有 API 密钥，而不会妨碍使用其他密钥的操作。</span><span class="sxs-lookup"><span data-stu-id="9d09a-110">Refresh or delete existing API keys without hampering operations using other keys.</span></span>

## <a name="why-do-we-support-scoped-api-keys"></a><span data-ttu-id="9d09a-111">为什么我们支持范围内的 API 密钥？</span><span class="sxs-lookup"><span data-stu-id="9d09a-111">Why do we support scoped API keys?</span></span>

<span data-ttu-id="9d09a-112">我们支持 API 密钥的范围是为了让你拥有更细粒度的权限。</span><span class="sxs-lookup"><span data-stu-id="9d09a-112">We support scopes for API keys to allow you to have more fine-grained permissions.</span></span> <span data-ttu-id="9d09a-113">以前，NuGet 为一个帐户提供了一个 API 密钥，这种方法有几个缺点：</span><span class="sxs-lookup"><span data-stu-id="9d09a-113">Previously, NuGet offered a single API key for an account, and that approach had several drawbacks:</span></span>

- <span data-ttu-id="9d09a-114">**一个 API 密钥控制所有包**。</span><span class="sxs-lookup"><span data-stu-id="9d09a-114">**One API key to control all packages**.</span></span> <span data-ttu-id="9d09a-115">若使用一个 API 密钥管理所有包，当多个开发人员处理不同包以及共享发布者帐户时，很难安全地共享密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-115">With a single API key that is used to manage all packages, it is difficult to securely share the key when multiple developers are involved with different packages, and when they share a publisher account.</span></span>
- <span data-ttu-id="9d09a-116">**要么所有权限，要么无任何权限**。</span><span class="sxs-lookup"><span data-stu-id="9d09a-116">**All permissions or none**.</span></span> <span data-ttu-id="9d09a-117">有权访问 API 密钥的任何人都拥有包的所有权限（发布、推送和取消列表）。</span><span class="sxs-lookup"><span data-stu-id="9d09a-117">Anyone with access to the API key has all permissions (publish, push and un-list) on the packages.</span></span> <span data-ttu-id="9d09a-118">在具有多个团队的环境中，这通常是不可取的。</span><span class="sxs-lookup"><span data-stu-id="9d09a-118">This is often not desirable in environment with multiple teams.</span></span>
- <span data-ttu-id="9d09a-119">**单个故障点**。</span><span class="sxs-lookup"><span data-stu-id="9d09a-119">**Single point of failure**.</span></span> <span data-ttu-id="9d09a-120">单个 API 密钥也意味着单个故障点。</span><span class="sxs-lookup"><span data-stu-id="9d09a-120">A single API key also means a single point of failure.</span></span> <span data-ttu-id="9d09a-121">如果密钥已泄露，则与该帐户有关的所有包都可能存在危险。</span><span class="sxs-lookup"><span data-stu-id="9d09a-121">If the key is compromised, all packages associated with the account could potentially be compromised.</span></span> <span data-ttu-id="9d09a-122">刷新 API 密钥是堵住漏洞，避免 CI/CD 工作流中断的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="9d09a-122">Refreshing the API key is the only way to plug the leak and avoid an interruption to your CI/CD workflow.</span></span> <span data-ttu-id="9d09a-123">此外，在某些情况下，你可能希望撤销某个人对 API 密钥的访问权限（例如，当员工离开组织时）。</span><span class="sxs-lookup"><span data-stu-id="9d09a-123">In addition, there may be cases when you want to revoke access to the API key for an individual (for example, when an employee leaves the organization).</span></span> <span data-ttu-id="9d09a-124">没有可以立即处理这种情况的有效方法。</span><span class="sxs-lookup"><span data-stu-id="9d09a-124">There isn’t a clean way to handle this today.</span></span>

<span data-ttu-id="9d09a-125">使用范围内的 API 密钥，我们尝试解决这些问题，同时确保现有的工作流不会中断。</span><span class="sxs-lookup"><span data-stu-id="9d09a-125">With scoped API keys, we try to address these problems while making sure that none of the existing workflows break.</span></span>

## <a name="acquire-an-api-key"></a><span data-ttu-id="9d09a-126">获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-126">Acquire an API key</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a><span data-ttu-id="9d09a-127">创建范围内的 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-127">Create scoped API keys</span></span>

<span data-ttu-id="9d09a-128">可以根据需要创建多个 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-128">You can create multiple API keys based on your requirements.</span></span> <span data-ttu-id="9d09a-129">API 密钥可以应用于一个或多个包，具有授予特定权限的不同范围，并具有与之相关的到期日期。</span><span class="sxs-lookup"><span data-stu-id="9d09a-129">An API key can apply to one or more packages, have varying scopes that grant specific privileges, and have an expiration date associated with it.</span></span>

<span data-ttu-id="9d09a-130">在以下示例中，你有一个名为 `Contoso service CI` 的 API 密钥，可用于为特定 `Contoso.Service` 包推送包，并且有效期为 365 天。</span><span class="sxs-lookup"><span data-stu-id="9d09a-130">In the following example, you have an API key named `Contoso service CI` that can be used to push packages for specific `Contoso.Service` packages, and is valid for 365 days.</span></span> <span data-ttu-id="9d09a-131">这是一个典型的情况，即同一组织中的不同团队处理不同的包，并且团队成员获得的密钥仅向他们授予正在处理的包的权限。</span><span class="sxs-lookup"><span data-stu-id="9d09a-131">This is a typical scenario where different teams within the same organization work on different packages, and the members of the team are provided the key that grants them privileges only for the package they are working on.</span></span> <span data-ttu-id="9d09a-132">到期用作一种防止密钥过时或遗忘的机制。</span><span class="sxs-lookup"><span data-stu-id="9d09a-132">The expiration serves as a mechanism to prevent stale or forgotten keys.</span></span>

![创建 API 密钥](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a><span data-ttu-id="9d09a-134">使用 glob 模式</span><span class="sxs-lookup"><span data-stu-id="9d09a-134">Use glob patterns</span></span>

<span data-ttu-id="9d09a-135">如果处理多个包并且需要管理大量包，则可以选择使用通配模式同时选择多个包。</span><span class="sxs-lookup"><span data-stu-id="9d09a-135">If you are working on multiple packages and have a large list of packages to manage, you can choose to use globbing patterns to select multiple packages together.</span></span> <span data-ttu-id="9d09a-136">例如，如果希望为 ID 以 `Fabrikam.Service` 开头的所有包的键授予特定的范围，则可以在“Glob 模式”文本框中指定 `fabrikam.service.*`  。</span><span class="sxs-lookup"><span data-stu-id="9d09a-136">For example, if you wish to grant specific scopes to a key for all packages whose ID starts with `Fabrikam.Service`, you could do this by specifying `fabrikam.service.*` in the **Glob pattern** text box.</span></span>

![创建 API 密钥](media/scoped-api-keys-glob-pattern.png)

<span data-ttu-id="9d09a-138">使用 glob 模式确定 API 密钥权限也适用于与 glob 模式匹配的新包。</span><span class="sxs-lookup"><span data-stu-id="9d09a-138">Using glob patterns to determine API key permissions also applies to new packages matching the glob pattern.</span></span> <span data-ttu-id="9d09a-139">例如，如果尝试推送名为 `Fabrikam.Service.Framework` 的新包，则可以使用之前创建的密钥执行此操作，因为该包与 glob 模式 `fabrikam.service.*` 匹配。</span><span class="sxs-lookup"><span data-stu-id="9d09a-139">For example, if you try to push a new package named `Fabrikam.Service.Framework`, you can do that with the key created previously, since the package matches the glob pattern `fabrikam.service.*`.</span></span>

## <a name="obtain-api-keys-securely"></a><span data-ttu-id="9d09a-140">安全地获取 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-140">Obtain API keys securely</span></span>

<span data-ttu-id="9d09a-141">为了安全起见，屏幕上永远不会显示新创建的密钥，只能使用“复制”按钮  。</span><span class="sxs-lookup"><span data-stu-id="9d09a-141">For security, a newly created key is never shown on the screen and is only available using the **Copy** button.</span></span> <span data-ttu-id="9d09a-142">同样，刷新页面后无法访问该密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-142">Similarly, the key is not accessible after the page is refreshed.</span></span>

![创建 API 密钥](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a><span data-ttu-id="9d09a-144">编辑现有 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-144">Edit existing API keys</span></span>

<span data-ttu-id="9d09a-145">你还可能希望在不更改密钥本身的情况下更新密钥权限和范围。</span><span class="sxs-lookup"><span data-stu-id="9d09a-145">You may also want to update the key permissions and scopes without changing the key itself.</span></span> <span data-ttu-id="9d09a-146">如果有一个针对单个包的具有特定范围的密钥，则可以选择向一个或多个其他包应用同一范围。</span><span class="sxs-lookup"><span data-stu-id="9d09a-146">If you have a key with specific scope(s) for a single package, you can choose to apply the same scope(s) on one or many other packages.</span></span>

![创建 API 密钥](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a><span data-ttu-id="9d09a-148">刷新或删除现有 API 密钥</span><span class="sxs-lookup"><span data-stu-id="9d09a-148">Refresh or delete existing API keys</span></span>

<span data-ttu-id="9d09a-149">帐户所有者可以选择刷新密钥，在这种情况下（对包的）权限、范围和到期日期保持不变，但是会发出一个新密钥，使旧密钥无法使用。</span><span class="sxs-lookup"><span data-stu-id="9d09a-149">The account owner can choose to refresh the key, in which case the permission (on packages), scope, and expiry remain the same, but a new key is issued making the old key unusable.</span></span> <span data-ttu-id="9d09a-150">这有助于管理过时密钥，或者有助于可能存在 API 密钥泄漏的情况。</span><span class="sxs-lookup"><span data-stu-id="9d09a-150">This is helpful in managing stale keys or where there is any potential for an API key leakage.</span></span>

![创建 API 密钥](media/scoped-api-keys-refresh.png)

<span data-ttu-id="9d09a-152">如果不再需要这些密钥，也可以选择删除这些密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-152">You may also choose to delete these keys if they are not needed anymore.</span></span> <span data-ttu-id="9d09a-153">删除密钥将移除密钥并使其无法使用。</span><span class="sxs-lookup"><span data-stu-id="9d09a-153">Deleting a key removes the key and makes it unusable.</span></span>

## <a name="faqs"></a><span data-ttu-id="9d09a-154">常见问题解答</span><span class="sxs-lookup"><span data-stu-id="9d09a-154">FAQs</span></span>

### <a name="what-happens-to-my-old-legacy-api-key"></a><span data-ttu-id="9d09a-155">我的旧（旧版）API 密钥会怎么样？</span><span class="sxs-lookup"><span data-stu-id="9d09a-155">What happens to my old (legacy) API key?</span></span>

<span data-ttu-id="9d09a-156">旧（旧版）API 密钥可继续使用，使用时间由你决定。</span><span class="sxs-lookup"><span data-stu-id="9d09a-156">Your old API key (legacy) continues to work and can work as long as you want it to work.</span></span> <span data-ttu-id="9d09a-157">但是，如果这些密钥已超过 365 天未被用于推送包，则将停用。</span><span class="sxs-lookup"><span data-stu-id="9d09a-157">However, these keys will be retired if they have not been used for more than 365 days to push a package.</span></span> <span data-ttu-id="9d09a-158">有关详细信息，请参阅博客文章[更改即将到期的 API 密钥](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html)。</span><span class="sxs-lookup"><span data-stu-id="9d09a-158">For more details, see the blog post [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span></span> <span data-ttu-id="9d09a-159">无法再刷新此密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-159">You can no longer refresh this key.</span></span> <span data-ttu-id="9d09a-160">需要删除旧密钥并改为创建新的范围内的密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-160">You need to delete the legacy key and create a new scoped key instead.</span></span>

> [!NOTE]
> <span data-ttu-id="9d09a-161">此密钥具有所有包的所有权限，并且永不过期。</span><span class="sxs-lookup"><span data-stu-id="9d09a-161">This key has all permissions on all the packages and it never expires.</span></span> <span data-ttu-id="9d09a-162">应该考虑删除此密钥并创建具有范围内权限和明确期限的新密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-162">You should consider deleting this key and creating new keys with scoped permissions and definite expiry.</span></span>

### <a name="how-many-api-keys-can-i-create"></a><span data-ttu-id="9d09a-163">我可以创建多少个 API 密钥？</span><span class="sxs-lookup"><span data-stu-id="9d09a-163">How many API keys can I create?</span></span>

<span data-ttu-id="9d09a-164">可以创建的 API 密钥数量没有限制。</span><span class="sxs-lookup"><span data-stu-id="9d09a-164">There is no limit on the number of API keys you can create.</span></span> <span data-ttu-id="9d09a-165">但我们建议保留易于管理的个数，这样你就不会获得许多过时密钥，而不知道密钥在何处以及谁在使用它们。</span><span class="sxs-lookup"><span data-stu-id="9d09a-165">However, we advise you to keep it to a manageable count so that you do not end up having many stale keys with no knowledge of where and who is using them.</span></span>

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a><span data-ttu-id="9d09a-166">我是否可以删除旧 API 密钥或立即停止使用？</span><span class="sxs-lookup"><span data-stu-id="9d09a-166">Can I delete my legacy API key or discontinue using now?</span></span>

<span data-ttu-id="9d09a-167">可以。</span><span class="sxs-lookup"><span data-stu-id="9d09a-167">Yes.</span></span> <span data-ttu-id="9d09a-168">你可以并且应该删除你的旧 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-168">You can--and you probably should--delete your legacy API key.</span></span>

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a><span data-ttu-id="9d09a-169">我是否可以找回错误删除的 API 密钥？</span><span class="sxs-lookup"><span data-stu-id="9d09a-169">Can I get back my API key that I deleted by mistake?</span></span>

<span data-ttu-id="9d09a-170">不是。</span><span class="sxs-lookup"><span data-stu-id="9d09a-170">No.</span></span> <span data-ttu-id="9d09a-171">删除后，你只能创建新密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-171">Once deleted, you can only create new keys.</span></span> <span data-ttu-id="9d09a-172">意外删除的密钥无法恢复。</span><span class="sxs-lookup"><span data-stu-id="9d09a-172">There is no recovery possible for accidentally deleted keys.</span></span>

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a><span data-ttu-id="9d09a-173">API 密钥刷新时是否可继续使用旧 API 密钥？</span><span class="sxs-lookup"><span data-stu-id="9d09a-173">Does the old API key continue to work upon API key refresh?</span></span>

<span data-ttu-id="9d09a-174">不是。</span><span class="sxs-lookup"><span data-stu-id="9d09a-174">No.</span></span> <span data-ttu-id="9d09a-175">刷新密钥后，将生成一个与旧密钥具有相同范围、权限和期限的新密钥。</span><span class="sxs-lookup"><span data-stu-id="9d09a-175">Once you refresh a key, a new key gets generated that has the same scope, permission, and expiry as the old one.</span></span> <span data-ttu-id="9d09a-176">旧密钥不复存在。</span><span class="sxs-lookup"><span data-stu-id="9d09a-176">The old key ceases to exist.</span></span>

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a><span data-ttu-id="9d09a-177">我可以为现有 API 密钥授予更多权限吗？</span><span class="sxs-lookup"><span data-stu-id="9d09a-177">Can I give more permissions to an existing API key?</span></span>

<span data-ttu-id="9d09a-178">你无法修改范围，但可以编辑适用的包列表。</span><span class="sxs-lookup"><span data-stu-id="9d09a-178">You cannot modify the scope, but you can edit the package list it is applicable to.</span></span>

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a><span data-ttu-id="9d09a-179">如何知道密钥是已过期还是即将过期？</span><span class="sxs-lookup"><span data-stu-id="9d09a-179">How do I know if any of my keys expired or are getting expired?</span></span>

<span data-ttu-id="9d09a-180">如果任何密钥过期，我们会通过页面顶部的警告消息通知你。</span><span class="sxs-lookup"><span data-stu-id="9d09a-180">If any key expires, we will let you know through a warning message at the top of the page.</span></span> <span data-ttu-id="9d09a-181">我们还会在密钥到期前十天向帐户持有者发送警告电子邮件，以便能够提前做好准备。</span><span class="sxs-lookup"><span data-stu-id="9d09a-181">We also send a warning e-mail to the account holder ten days before the expiration of the key so that you can act on it well in advance.</span></span>