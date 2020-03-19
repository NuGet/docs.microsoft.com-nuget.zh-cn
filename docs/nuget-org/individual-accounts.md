---
title: 个人帐户 - NuGet.org
description: 需要 NuGet.org 上的个人帐户以发布包
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428629"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org 上的个人帐户

必须创建个人帐户才能在 NuGet.org 上发布和管理包。

## <a name="individual-accounts-vs-organization-accounts"></a>个人帐户与组织帐户

个人（用户）帐户是你在 NuGet.org 上的标识，可以是任意数量的组织的成员。 包可以属于组织帐户，也可以属于个人帐户。 包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。

组织帐户具有一个或多个个人帐户作为其成员。 这些成员可以管理一组包，同时保持所有权的单一标识。

## <a name="add-a-new-individual-account"></a>添加新的个人帐户

要创建 NuGet.org 帐户，需要具备 Microsoft 个人帐户 (MSA) 或 Azure Active Directory (AAD) 帐户。 如果没有帐户，请[创建](https://signup.live.com)帐户。 如果拥有 MSA 或 AAD 帐户，请执行以下步骤。

1. 转到 [NuGet.org 登录页](https://www.nuget.org/users/account/LogOn)。

1. 单击“Microsoft 登录”按钮  。

1. 输入 Microsoft 帐户或 Azure Active Directory 帐户详细信息。

1. 请单击“是”以接受要授予 NuGet.org 应用程序的权限   。

   ![授予 NuGet.org 权限](media/nuget-org-permissions.png)

1. 此时系统将重定向至 nuget.org 并要求注册用户名  。

1. 在输入框中指定用户名。 请注意，用户名需区分大小写，并且以后无法更改或重命名  。

   ![在 NuGet.org 上指定用户名](media/nuget-org-register.png) 

1. 单击“注册”按钮  。

现在 NuGet.org 帐户已成功创建。 可以在[帐户设置](https://www.nuget.org/account)页面执行帐户管理。

## <a name="enable-two-factor-authentication-2fa"></a>启用双因素身份验证 (2FA)

双因素身份验证 (2FA) 是登录网站或应用时采用的额外安全保障。 由于 2FA，你必须使用 Microsoft 帐户 (MSA) 进行登录，并另外提供一种只有你知道或有权访问的身份验证形式。 为了更好地保护你的帐户，请启用双因素身份验证（推荐）。

1. 登录到你的帐户后，打开个人资料，然后选择“登录帐户”下的“启用”   。

   ![启用 2FA](media/nuget-org-register-2fa.png)

   随即显示一条消息，提示你在下次登录 nuget.org  时，系统会要求提供其他凭据。

2. 若要在此时完成身份验证，请先注销，然后再次登录。

3. 登录后，选择文本或电子邮件作为第二种形式的身份验证。

   验证已与 Microsoft 帐户关联的电话号码或电子邮件。 可能需要为你的帐户输入一个新的电话号码或电子邮件。 如果是这样，请按照说明输入所需信息，然后单击“下一步”  。

   ![启用 2FA](media/nuget-org-sign-in-2fa.png)

4. 检查设备或电子邮件帐户，然后输入刚刚收到的代码。

   ![启用 2FA](media/nuget-org-enter-code-2fa.png)

5. 按照任何其他说明完成双因素身份验证。

> [!Tip]
> 对于可能链接了用于登录 NuGet.org 的 Microsoft 帐户的其他帐户或服务，为 NuGet.org 帐户启用 2FA 不会影响它们的身份验证设置。

## <a name="delete-a-nugetorg-account"></a>删除 NuGet.org 帐户

有关其他帐户相关任务（例如删除 NuGet.org 帐户）的帮助，请参阅 [NuGet.org 帐户管理](nuget-org-faq.md#nugetorg-account-management)。
