---
title: NuGet.org 常见问题解答
description: 有关使用 NuGet 库的常见问题和解答。
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813736"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org 常见问题解答

## <a name="license-terms"></a>许可条款

如果包未提供特定许可信息，有哪些默认许可条款？ 

每个包都需要受包中所含条款约束。 你应该在访问、下载或获取任何包前查看适用条款。 在 NuGet.org 中，请使用包页面中的“许可信息”链接  。

如果包未指定许可条款，请直接通过 NuGet.org 包页面上的“联系所有者”链接与包所有者联系  。 Microsoft 不向用户授予任何第三方包提供程序的知识产权许可，同时不对第三方提供的信息承担任何责任。

## <a name="managing-packages-on-nugetorg"></a>管理 NuGet.org 上的包

在上传包元数据后是否可以再对其进行编辑？ 

NuGet 建议对所有的包签名。 包签名的设计原则是已签名包的内容不得改变，nuspec 也包括在内。 编辑包元数据会使 nuspec 发生更改，导致现有签名无效。 我们建议在创建包后修改现有工作流，这样则无需编辑包元数据。

请注意，列出的包依赖项从包本身自动生成，并且无法进行编辑。

此外，要测试和验证包，同时不在公共库中提供此包，最好将包上传到[ int.nugettest.org](https://int.nugettest.org)。 API 终结点： https://apiint.nugettest.org/v3/index.json

**我能否删除发布到 NuGet.org 的包？**

通常，我们不支持删除发布到 NuGet.org 的包。详细阅读我们的[包删除策略](policies/deleting-packages.md)。

是否可以为以后发布的包预留名称？ 

可以。 通过为帐户请求包 ID 前缀可以在 [NuGet.org](https://www.nuget.org/) 中预留包 ID。 若要请求包 ID 前缀，请按照[文档](id-prefix-reservation.md)中的说明操作。

如何声明包的所有权？ 

请参阅[在 NuGet.org 上管理包所有者](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)。

如何与违反我的软件许可的包所有者进行交涉？ 

我们鼓励 NuGet 社区合作解决包所有者和其他软件所有者之间可能出现的任何争议。 我们制定了周密的[争议解决流程](policies/dispute-resolution.md)，要求 NuGet.org 管理员调解之前应遵循此流程。

是否建议将测试包上传到 NuGet.org？ 

对于测试目的，可以使用 [int.nugettest.org](https://int.nugettest.org)，或使用备用的公共 NuGet 服务器，如 [myget.org](https://myget.org) 或 [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)。

请注意，上传到 int.nugettest.org 的包可能不会保留。

可上传到 NuGet.org 的最大包大小是多少？ 

NuGet.org 允许的最大包大小为 250 MB，但我们建议尽可能将包保持在 1 MB 以下，通过依赖项将包链接在一起。 依据经验，仅包含一个程序集的包可以避免冲突。

NuGet 使用 HTTP 下载包，因此较大包比较小包有更高的安装失败风险。

依赖项可以在多个包之间进行共享，这样可减小 NuGet 包使用者的总下载大小。

依赖项通常是静态的，永远不会更改。 修复代码中的 bug 时，可能无需更新依赖项。 如果捆绑依赖项，最终将导致每一次都需要重新传输更大的包。 通过将 NuGet 包拆分成相关的依赖项，包使用者可以获得更细化的更新。

## <a name="nugetorg-not-accessible"></a>NuGet.org 不可访问

为何无法从 NuGet.org 下载包或向其中上传包？ 

首先，请确保使用的是最新版本的 NuGet。 如果该版本仍然失败，请[联系支持人员](https://www.nuget.org/policies/Contact)，并提供其他连接故障排除信息，包括：

- 使用的 NuGet 版本
- 使用的包源
- 详细还原日志
- MTR 或 Fiddler 跟踪（见下文）
- 所在地理区域
- 计算机是否设置了代理或防火墙？
- 计算机是否位于云提供商的数据中心（Azure、AWS 等）？ 如果是，请提供此提供商名称和区域。

捕获 MTR： 

- 下载 [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download)。
- 输入 `api.nuget.org` 作为主机名，然后单击“启动”  。
- 等待，直到“已发送”列 >= 100  。

    ![捕获 MTR](media/mtr.png)

- 将文本复制到剪贴板。

捕获 Fiddler： 

- 安装最新版本的 [Fiddler](https://www.telerik.com/download/fiddler)。
- 启动 Fiddler，使用“文件”>“捕获流量”菜单禁用捕获流量  。
- 删除所有会话（选中列表中的所有项，按 Delete 键  ）。
- 配置 Fiddler 以捕获 HTTPS 流量，具体操作方式为：打开“工具”>“Fiddler 选项...”菜单，勾选“HTTPS”选项卡中的“解密 HTTPS 流量”    。
- 关闭 Visual Studio。
- 启用“文件”>“捕获流量”菜单  。
- 启动 Visual Studio 或 nuget.exe.exe，执行当前未运行的操作。 Fiddler 中应显示出这些操作所产生的流量。
- 操作运行结束后，使用“文件”>“保存”>“所有会话”来存储捕获的会话  。

注意：若要通过 Fiddler 路由 NuGet，可能需要将 `HTTP_PROXY` 环境变量设置为 `http://127.0.0.1:8888`。

如果该操作失败，请尝试[该 StackOverflow 文章中提到的方法](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)。

## <a name="nugetorg-account-management"></a>NuGet.org 帐户管理

### <a name="how-to-recover-nugetorg-password-login"></a>如何恢复 NuGet.org 密码登录？

请注意，[NuGet.org 密码登录已经停止使用](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html)，当前登录 NuGet.org 的唯一方式是使用 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。 但是，在无法访问关联的 MSA/AAD 帐户的情形下，可能需要通过密码登录恢复 NuGet.org 帐户。 这种情况下，请执行以下步骤。
- **要求：** 需要有权访问与要恢复密码的帐户相关联的电子邮件。
- 转到[“忘记密码”页面](https://www.nuget.org/account/ForgotPassword)
- 输入与要恢复的 NuGet.org 帐户相关联的电子邮件地址  。
- 单击“发送”按钮  。
- 指定的电子邮件地址帐户会收到一封电子邮件，其中包含密码重置链接。 单击此链接并设置新密码。 如果未找到该邮件，请查看“垃圾邮件”文件夹。
- 完成后，现在可以使用用户名/密码登录 NuGet。
- 要通过用户名/密码登录，请使用 [NuGet.org 帐户登录页面](https://www.nuget.org/users/account/LogOn)上的“使用 NuGet.org 帐户登录”链接  。

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>哪个 Microsoft 帐户已链接到 NuGet.org 帐户？

如果忘记了与 NuGet.org 帐户关联的 Microsoft 帐户，请按照以下步骤获取帮助。
1. 转到 [NuGet.org 登录页面](https://www.nuget.org/users/account/LogOn)，并单击“需要登录协助?”链接  。
1. 此操作会弹出一个帮助对话框。 按照该对话框中的步骤，找出与 NuGet.org 帐户的关联的 Microsoft 帐户。

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>如何更改用于登录 NuGet.org 的 Microsoft 帐户？
要更改登录 NuGet.org 所用的 Microsoft 帐户，请执行以下步骤。 假设电子邮件为 `account1@outlook.com` 的 Microsoft 帐户已关联到用户名为 `MyNuGetAccount` 的 NuGet.org 帐户。 现在需要将登录帐户更改为电子邮件为 `account2@outlook.com` 的另一 Microsoft 帐户
1. 转到[登录页面](https://www.nuget.org/users/account/LogOn)，单击“Microsoft 登录”，然后使用当前关联的 Microsoft 帐户（即 `account1@outlook.com`）登录   。
1. 登录后，请转到[帐户设置](https://www.nuget.org/account)页面。
1. 展开“登录帐户”部分  。 单击“更改帐户”按钮  。
1. 系统会重定向至 Microsoft 登录页面。 请使用要更改为关联帐户的帐户登录，即 `account2@outlook.com`。**注意**：登录过程中，可能需要单击“注销并使用另一个帐户登录”，才能使用其他 Microsoft 帐户登录  。
1. 如果看到如下类似错误，请查看 [Microsoft 帐户已链接到另一个 NuGet.org 帐户](#microsoft-account-is-linked-with-another-nugetorg-account)，了解详细信息。
    >_无法将此 Microsoft 帐户更新为“account2 <account2@outlook.com>”。原因可能是该帐户已链接到另一个 NuGet 帐户。有关详细信息，请联系支持人员。_

1. 使用第二个帐户成功登录后，系统会重定向到 NuGet.org 帐户设置页面，现在应能看到新的 Microsoft 帐户关联作为登录帐户。 之后登录 NuGet.org 时应使用此帐户。

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft 帐户已链接到另一个 NuGet.org 帐户。

尝试更改 Microsoft 登录时可能出现如下错误：
> _无法将此 Microsoft 帐户更新为“account2 <account2@outlook.com>”。原因可能是该帐户已链接到另一个 NuGet 帐户。有关详细信息，请联系支持人员。_

假设对于用户名为 `MyNuGetAccount1` 的 NuGet.org 用户，要将其 Microsoft 帐户登录从 `account1@outlook.com` 更改为电子邮件为 `account2@outlook.com` 的另一 Microsoft 帐户。 更改过程中出现上述错误。

**上述错误表示什么意思？**

该错误表示要更改到的 Microsoft 帐户已有一个与之关联的 NuGet.org 帐户，即上例中电子邮件为 `<account2@outlook.com>` 的 Microsoft 帐户与另一个 NuGet.org 帐户（例如，用户名为 `MyNuGetAccount2`）相关联。

无法将关联登录更改为已连接到另一个 NuGet.org 帐户的 Microsoft 帐户。

**如果忘记了另一个 NuGet.org 帐户，如何才能将其找出？**

在[登录页面](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "登录页面")上使用第二个 Microsoft 帐户登录。 这会登录到当前与第二个 Microsoft 帐户相关联的 NuGet.org 帐户。 然后可以通过此帐户查看已上传的包和进行帐户管理。

**我不太关注第二个 NuGet.org 帐户，我希望将第二个 Microsoft 帐户更改为第一个 NuGet.org 帐户的登录名。我该怎么办？**

如果不关注第二个 NuGet.org 帐户，并仍希望重新使用已关联的 Microsoft 帐户（电子邮件为 `account2@outlook.com`）， 

可以通过删除该 NuGet.org 帐户，解除其与此 Microsoft 帐户之间的关联。
1. 对于第二个 NuGet.org 帐户 `MyNuGetAccount2`，请执行[删除用户](#how-to-delete-my-nugetorg-account)的步骤。 
1. 删除此帐户后，可以重试[更改 Microsoft 帐户登录](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)的步骤。

**等一下，我也关注第二个帐户。我不想失去此帐户，但同时也想更改第一个帐户的关联帐户。**

为此，需要创建/使用第三个 Microsoft 帐户，假设该帐户的电子邮件为 `account3@outlook.com`。 
1. 首先应使用第二个 Microsoft 帐户 `account2@outlook.com` 登录 NuGet.org。按照以上步骤更改关联登录并将第三个 Microsoft 帐户与此 NuGet.org 帐户关联。
1. 完成后，电子邮件为 `account2@outlook.com` 的第二个 Microsoft 帐户即可关联到第一个 NuGet.org 帐户 (`MyNuGetAccount1`)。 按照上述相同步骤将 Microsoft 帐户更改为第二个 Microsoft 帐户。

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>使用 Microsoft 帐户登录时显示电子邮件已链接到另一个 Microsoft 帐户

尝试使用 Microsoft 帐户（例如，电子邮件为 `account1@outlook.com` 的帐户）登录时，可能出现如下错误：
> 电子邮件为 "account1@outlook.com" 的帐户已链接到另一个 Microsoft 帐户  。
>
>  在帐户设置中可以更新已链接的 Microsoft 帐户。

**上述错误表示什么意思？**

在 NuGet.org 上创建帐户后，该帐户具有一个关联的通信电子邮件地址。 此地址通常与所关联 Microsoft 帐户的电子邮件地址相同。 但是，可以选择指定不同的电子邮件地址进行通信。 因此，从技术上讲，可以将另一个 Microsoft 帐户（例如电子邮件为 `account2@outlook.com` 的帐户）链接到通信电子邮件地址为 `account1@outlook.com` 的 NuGet.org 帐户。

所以，上述错误表示已存在一个通信电子邮件地址为 `account1@outlook.com` 的 NuGet.org 帐户，但该帐户已关联到电子邮件地址不是 `account1@outlook.com` 的另一个 Microsoft 帐户  。

如何查找哪个 Microsoft 帐户已链接到此 NuGet.org 帐户？ 

应该按照[登录协助](#which-microsoft-account-is-linked-to-my-nugetorg-account)流程找出哪个 Microsoft 帐户已链接到电子邮件地址为 `account1@outlook.com` 的 NuGet.org 帐户。

**我想要使用我的 Microsoft 帐户替换已关联的 Microsoft 帐户**

按照[无法使用 Microsoft 登录，如何恢复 NuGet.org 帐户](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)部分中的步骤将 Microsoft 帐户与现有 NuGet.org 帐户相关联。

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>无法使用 Microsoft 登录，如何恢复 NuGet.org 帐户？

如果尝试使用[登录帮助](#which-microsoft-account-is-linked-to-my-nugetorg-account) , 但无权访问与 NuGet.org 帐户关联的 Microsoft 帐户，请按照下面的步骤将新的 Microsoft 帐户链接到你的 NuGet.org 帐户。
1. **要求**：有权访问某 Microsoft 帐户，此帐户并未关联到任何现有 NuGet.org 帐户。 如果没有帐户，请[创建](https://signup.live.com)帐户。
2. 如果忘记了 NuGet.org 帐户的用户名和密码，请按照[恢复密码登录的步骤](#how-to-recover-nugetorg-password-login)操作。
3. 通过用户名/密码登录方法[登录 NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。
4. 登录后会弹出如下所示的对话框。 这是密码终止对话框。
5. **注意**：请忽略有关使用指定 Microsoft 帐户登录的说明。 现在可以将你的 NuGet.org 帐户链接到任何其他 Microsoft 登录名。
6. 单击“Microsoft 登录”按钮，然后按步骤 1 所述，使用具有访问权限的 Microsoft 帐户登录  。
7. 现在，你的帐户将链接到新 Microsoft 帐户，你可以使用它来登录 NuGet.org。

    ![MSA 链接对话框](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>如何将 NuGet.org 帐户转换为组织？

如要将帐户转换为组织帐户，且此帐户已与 Microsoft 帐户登录关联，请按照 [nuget org 上的组织](organizations-on-nuget-org.md)文档中的步骤操作。

但是，如果你的 NuGet.org 帐户未关联到 Microsoft 帐户，则可以按照以下步骤将此帐户转换为组织。
1. **要求**：需要首先在 NuGet.org 上创建一个个人帐户，以用作组织帐户的管理员。 如果没有，请[创建新的 NuGet.org 帐户](individual-accounts.md)
2. 如果使用密码登录，请按照[此处所述的步骤](#how-to-recover-nugetorg-password-login)为你的 NuGet.org 帐户恢复密码登录，否则请跳过此步骤。
3. 通过用户名/密码登录方法[登录 NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount)。
4. 登录后会弹出如下所示的对话框。 这是密码终止对话框。 
    > [!Important]
    > 请忽略此对话框，切勿单击“Microsoft 登录”按钮   。

5. 转到 [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)。 这会将此 NuGet.org 帐户转换为组织帐户，且无需链接到 Microsoft 帐户。
6. 为 NuGet.org 个人帐户/步骤 1 中创建的帐户指定管理员用户名。
7. 按照说明将此帐户转换为组织帐户。

    ![MSA 链接对话框](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>出现有关具有非托管组合的 AAD 帐户的 NuGet.org 登录问题？

使用电子邮件帐户域 (@yourdomain.com) 登录过程中如果出现类似如下的错误，请参阅以下步骤恢复 NuGet.org 帐户。

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**登录过程中出现的“非托管”状态是什么？为什么会出现这种情况？** 

你的帐户似乎在之前注册为 Microsoft 个人帐户，且其使用正常，但现在此帐户似乎已在 Azure Active Directory（用于对 Microsoft 帐户执行身份验证的标识符）中注册为“非托管”租户。 

出现此情况的原因可能是你或你所在组织的其他人员（电子邮件为 @yourdomain.com）注册了某个 AAD 集成服务，或者进行了 [Azure Active Directory 自助注册](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup)，这会对所使用的 Microsoft 帐户域（对你而言为 @yourdomain.com）创建一个“非托管”租户。 

**怎样才可以恢复帐户？**

当前，我们 (NuGet.org) 无法使用 Azure Active Directory 中含有此类“非托管”租户帐户对帐户进行身份验证。 我们正在寻找一种更佳的方式来对此类帐户进行身份验证。

如果要使用 Microsoft 帐户 (@yourdomain.com) 登录 NuGet.org，你（或你所在公司的管理员）需要通过执行 DNS 验证声明 AAD 所有者，以对电子邮件地址为“@yourdomain.com”的用户进行身份验证。 请按照 Azure Active directory 文档[域管理员接管](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover)中的步骤操作。 完成后，应能开始正常登录。

**我不想使用这种方法，还有什么其他方法可以恢复帐户？**

可以[创建](https://www.microsoft.com/account)一个新的 Microsoft 帐户（其电子邮件未与 @yourdomain.com 关联）  。 请按照[恢复 NuGet.org 帐户](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)部分所述的步骤操作。

### <a name="how-do-i-change-my-nugetorg-account-username"></a>如何更改 NuGet.org 帐户用户名？

无法更改。 根据策略，我们不允许更改用户名。 此外，对于已[根据包所有者定义包信任策略](../consume-packages/installing-signed-packages.md#trust-package-owners)的用户，这是一项重大更改。 更改用户名的唯一方式是创建采用所需用户名的新帐户。 创建新帐户之前，我们建议删除现有帐户，否则便可能无法重复使用已注册的 Microsoft 帐户。
> [!Important]
> 删除用户仍会保留 `username`  。 你将无法重复使用相同的用户名，即使更改大小写也不例外  。 例如，创建用户名为 `mycoolname` 的用户然后删除此用户后，要将此用户名改为 `MyCoolName`（大小写更改）是不可实现的。

按照删除 [NuGet.org 帐户](#how-to-delete-my-nugetorg-account)部分中所述的步骤使用正确用户名[注册新用户](individual-accounts.md)。

### <a name="how-to-delete-my-nugetorg-account"></a>如何删除 NuGet.org 帐户？

请注意，要删除帐户，我们建议将你作为其唯一所有者的包的所有权进行转让。 要了解如何执行此操作，请阅读有关[管理包所有者](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)的更多信息。 这有助于我们加速处理请求。

如果要将帐户转换为组织，请按照[将 NuGet.org 帐户转换为组织](#how-to-transform-my-nugetorg-account-to-an-organization)中所述的步骤进行操作。

> [!Important]
> 删除用户会导致以下结果：
>  1. 用户名将被保留，其他人无法重用它来创建个人帐户或组织帐户
>  1. 撤销关联的 API 密钥。 
>  1. 删除作为任何子包所有者的帐户。
>  1. 将所有之前存在的 ID 前缀预留与此帐户取消关联。
>  1. 删除作为任何组织成员的帐户。

请按照以下步骤继续进行帐户删除。
1. 使用要删除的帐户[登录到 NuGet.org](https://www.nuget.org/users/account/LogOn)。
2. 单击此 URL：[https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)，然后按照步骤提交帐户删除请求。

我们的客户支持人员将处理请求并执行帐户删除操作。
