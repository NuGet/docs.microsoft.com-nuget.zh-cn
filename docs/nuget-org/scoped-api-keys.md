---
title: 范围内的 API 密钥
description: 控制用于推送包的 API 密钥
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901585"
---
# <a name="scoped-api-keys"></a>范围内的 API 密钥

为了使 NuGet 成为一个更安全的包分发环境，可以通过添加范围来控制 API 密钥。

借助向 API 密钥提供范围的功能可更好地控制 API。 可以执行以下操作：

- 创建多个范围内的 API 密钥，可用于具有不同到期时间表的不同包。
- 安全地获取 API 密钥。
- 编辑现有 API 密钥以更改包适用性。
- 刷新或删除现有 API 密钥，而不会妨碍使用其他密钥的操作。

## <a name="why-do-we-support-scoped-api-keys"></a>为什么我们支持范围内的 API 密钥？

我们支持 API 密钥的范围是为了让你拥有更细粒度的权限。 以前，NuGet 为一个帐户提供了一个 API 密钥，这种方法有几个缺点：

- **一个 API 密钥控制所有包**。 若使用一个 API 密钥管理所有包，当多个开发人员处理不同包以及共享发布者帐户时，很难安全地共享密钥。
- **要么所有权限，要么无任何权限**。 有权访问 API 密钥的任何人都拥有包的所有权限（发布、推送和取消列表）。 在具有多个团队的环境中，这通常是不可取的。
- **单个故障点**。 单个 API 密钥也意味着单个故障点。 如果密钥已泄露，则与该帐户有关的所有包都可能存在危险。 刷新 API 密钥是堵住漏洞，避免 CI/CD 工作流中断的唯一方法。 此外，在某些情况下，你可能希望撤销某个人对 API 密钥的访问权限（例如，当员工离开组织时）。 没有可以立即处理这种情况的有效方法。

使用范围内的 API 密钥，我们尝试解决这些问题，同时确保现有的工作流不会中断。

## <a name="acquire-an-api-key"></a>获取 API 密钥

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>创建范围内的 API 密钥

可以根据需要创建多个 API 密钥。 API 密钥可以应用于一个或多个包，具有授予特定权限的不同范围，并具有与之相关的到期日期。

在以下示例中，你有一个名为 `Contoso service CI` 的 API 密钥，可用于为特定 `Contoso.Service` 包推送包，并且有效期为 365 天。 这是一个典型的情况，即同一组织中的不同团队处理不同的包，并且团队成员获得的密钥仅向他们授予正在处理的包的权限。 到期用作一种防止密钥过时或遗忘的机制。

![创建 API 密钥](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>使用 glob 模式

如果处理多个包并且需要管理大量包，则可以选择使用通配模式同时选择多个包。 例如，如果希望为 ID 以 `Fabrikam.Service` 开头的所有包的键授予特定的范围，则可以在“Glob 模式”文本框中指定 `fabrikam.service.*`。

![创建 API 密钥 - 2](media/scoped-api-keys-glob-pattern.png)

使用 glob 模式确定 API 密钥权限也适用于与 glob 模式匹配的新包。 例如，如果尝试推送名为 `Fabrikam.Service.Framework` 的新包，则可以使用之前创建的密钥执行此操作，因为该包与 glob 模式 `fabrikam.service.*` 匹配。

## <a name="obtain-api-keys-securely"></a>安全地获取 API 密钥

为了安全起见，屏幕上永远不会显示新创建的密钥，只能使用“复制”按钮。 同样，刷新页面后无法访问该密钥。

![创建 API 密钥 - 3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>编辑现有 API 密钥

你还可能希望在不更改密钥本身的情况下更新密钥权限和范围。 如果有一个针对单个包的具有特定范围的密钥，则可以选择向一个或多个其他包应用同一范围。

![创建 API 密钥 - 4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>刷新或删除现有 API 密钥

帐户所有者可以选择刷新密钥，在这种情况下（对包的）权限、范围和到期日期保持不变，但是会发出一个新密钥，使旧密钥无法使用。 这有助于管理过时密钥，或者有助于可能存在 API 密钥泄漏的情况。

![创建 API 密钥 - 5](media/scoped-api-keys-refresh.png)

如果不再需要这些密钥，也可以选择删除这些密钥。 删除密钥将移除密钥并使其无法使用。

## <a name="faqs"></a>常见问题解答

### <a name="what-happens-to-my-old-legacy-api-key"></a>我的旧（旧版）API 密钥会怎么样？

旧（旧版）API 密钥可继续使用，使用时间由你决定。 但是，如果这些密钥已超过 365 天未被用于推送包，则将停用。 有关详细信息，请参阅博客文章[更改即将到期的 API 密钥](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html)。 无法再刷新此密钥。 需要删除旧密钥并改为创建新的范围内的密钥。

> [!NOTE]
> 此密钥具有所有包的所有权限，并且永不过期。 应该考虑删除此密钥并创建具有范围内权限和明确期限的新密钥。

### <a name="how-many-api-keys-can-i-create"></a>我可以创建多少个 API 密钥？

可以创建的 API 密钥数量没有限制。 但我们建议保留易于管理的个数，这样你就不会获得许多过时密钥，而不知道密钥在何处以及谁在使用它们。

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>我是否可以删除旧 API 密钥或立即停止使用？

是。 你可以并且应该删除你的旧 API 密钥。

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>我是否可以找回错误删除的 API 密钥？

不能。 删除后，你只能创建新密钥。 意外删除的密钥无法恢复。

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>API 密钥刷新时是否可继续使用旧 API 密钥？

不能。 刷新密钥后，将生成一个与旧密钥具有相同范围、权限和期限的新密钥。 旧密钥不复存在。

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>我可以为现有 API 密钥授予更多权限吗？

你无法修改范围，但可以编辑适用的包列表。

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>如何知道密钥是已过期还是即将过期？

如果任何密钥过期，我们会通过页面顶部的警告消息通知你。 我们还会在密钥到期前十天向帐户持有者发送警告电子邮件，以便能够提前做好准备。