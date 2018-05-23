---
title: 在 nuget.org 上的组织
description: 在 nuget.org 上的组织可帮助你管理的组或在团队中，公司环境发布的包。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
---
# <a name="organization-on-nugetorg"></a>在 nuget.org 上的组织

组织启用企业和开放源代码项目，在使用单个 nuget.org 标识包中进行协作。 对于包使用者，组织帐户将显示与 nuget.org 上的现有用户帐户相同。

## <a name="user-accounts-vs-organization-accounts"></a>与组织帐户的用户帐户

你的用户帐户为你的身份在 nuget.org，可以为任意数量的组织的成员。 包可以属于像它可以属于一个用户帐户的组织帐户。 包使用者看不到的用户帐户或组织帐户之间存在任何差异： 这两项以包的形式出现`owners`。

组织帐户具有作为其成员的一个或多个用户帐户。 在保持所有权的单个身份的同时，这些成员可以管理一组包。

## <a name="adding-a-new-organization"></a>添加新的组织

若要添加新的组织，选择你的帐户上 nuget.org，然后选择**管理组织...** 菜单命令：

![对于管理器的组织在 nuget.org 上的菜单选项](media/org-manage-option.png)

在下一页上，选择**添加新的组织**按钮：

![若要创建新的组织在 nuget.org 上的按钮](media/org-add-new-option.png)

在下一页上，提供组织名称和电子邮件地址。 因为组织帐户共享用户帐户相同的命名空间，必须从其他任何现有的组织或用户帐户不同的组织名称。 电子邮件地址必须也是唯一的所有帐户。

![在 nuget.org 上添加新的组织页](media/org-add-new-page.png)

组织帐户创建后，你是管理员和可以提交为组织的包并添加组织成员。

### <a name="transform-existing-account-to-an-organization"></a>转换到组织的现有帐户

> [!Warning]
> 是不可逆的帐户转换： 无法转换回用户帐户的组织。

如果您要为团队使用单个用户帐户管理包，并且想要将该帐户转换为组织，使用**转换你的组织帐户**选项**管理组织**页：

![在 nuget.org 上的选项将组织现有的帐户](media/org-transform-option.png)

在下一页上，指定不同的用户帐户分配为管理员的组织，然后选择**转换**。

![输入用于转换到组织的用户帐户的信息](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理组织成员

作为组织管理员，您可以通过提供每个成员 nuget.org 中添加成员*用户帐户名*; 不能使用电子邮件地址。 然后，你将标记为协作者或具有以下权限的管理员每个成员：

| 权限 | 协作者 | 管理员 |
| --- | --- | --- |
| 管理组织的包<br/>（提交新的包、 更新或不列出现有包） | 是 | 是 |
| 更改组织元数据<br/>（电子邮件地址，通知设置） | 否 | 是 |
| 管理组织成员 | 否 | 是 |
| 请求或组织包 co-ownership 请求处理 | 否 | 是 |

## <a name="managing-packages"></a>管理包

你可以查看所有包在你的帐户和你其中是成员的所有组织[管理包](https://www.nuget.org/account/Packages)页。 若要查看特定于你的帐户或任何特定的组织的包，请使用帐户筛选器在顶部页面右上角。

![与帐户筛选器的管理包](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>将包传输到组织
如果你想要将某些包传输到新创建的组织，则可以通过做到请求要共同拥有包的组织帐户，然后删除自己作为所有者。 如果你是组织的管理员，则无需接受所有权确认。 但是，如果你是协作者，作为所有者添加组织需要一个接受所有权的管理员。

## <a name="publishing-packages"></a>发布包

你需要将包发布到组织，如将包发布到的用户帐户： 通过直接将包上载到 nuget.org 或通过将包推送`nuget push`或`dotnet nuget push`CLI 命令。

### <a name="uploading-packages"></a>正在上载包

当你将新的程序包直接上载上[nuget.org 上载](https://www.nuget.org/packages/manage/upload)页上，你为用户或组织帐户分配的包所有者：

![上载包帐户选项](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 密钥

若要推送包`nuget push`或`dotnet nuget push`CLI 命令，你必须获取 API 密钥所需的这些命令。 有关详细信息，请参阅[发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。

在创建新的 API 密钥，选择相应的组织中**包所有者**下拉列表。 你创建任何 API 密钥是仅适用于选组织：

![使用帐户选项的 API 密钥](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>删除组织

作为用户，你可以删除自己的组织中通过选择`X`按钮的你的组织的成员资格所示：

![从组织中删除用户帐户](media/org-remove-self-option.png)

管理员可以从组织，包括其他管理员删除任何成员。 如果你组织的唯一管理员，不能删除自己，除非以管理员身份添加其他成员。

### <a name="deleting-an-organization-account"></a>删除组织帐户

此功能即将推出。
