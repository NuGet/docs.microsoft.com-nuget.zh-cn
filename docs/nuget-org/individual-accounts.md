---
title: 个人帐户
description: 需要 NuGet.org 上的个人帐户以发布包
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427132"
---
# <a name="individual-accounts"></a>个人帐户

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
