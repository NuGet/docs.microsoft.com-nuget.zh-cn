---
title: 在 nuget.org 上的组织
description: Nuget.org 上的组织可帮助你管理按组或团队，公司环境中发布的包。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551223"
---
# <a name="organization-on-nugetorg"></a>在 nuget.org 上的组织

组织启用企业和开放源代码项目，在使用单个 nuget.org 标识包中进行协作。 对于包使用者，组织帐户将显示与 nuget.org 上的现有用户帐户相同。

## <a name="user-accounts-vs-organization-accounts"></a>与组织帐户的用户帐户

你的用户帐户为你在 nuget.org 上的身份，可以为任意数量的组织的成员。 包可以属于一个组织帐户像它只能属于一个用户帐户。 包使用者未看到用户帐户或组织帐户之间的任何差异： 这两项以包的形式出现`owners`。

组织帐户作为其成员上具有一个或多个用户帐户。 这些成员可以管理一组包，同时保持所有权的单一标识。

## <a name="adding-a-new-organization"></a>正在添加新组织

若要添加新的组织，选择你的帐户在 nuget.org 中，然后选择**管理组织...** 菜单命令：

![在 nuget.org 上的管理器组织的菜单选项](media/org-manage-option.png)

在下一页上，选择**添加新组织**按钮：

![若要创建新的组织在 nuget.org 上的按钮](media/org-add-new-option.png)

在下一步页上，提供组织名称和电子邮件地址。 因为组织帐户共享相同的命名空间的用户帐户，组织名称必须不同于任何其他现有组织或用户帐户。 电子邮件地址必须也是唯一的所有帐户。

![在 nuget.org 上添加新组织页](media/org-add-new-page.png)

组织帐户创建后，您是管理员并可以提交为组织的包并添加组织的成员。

### <a name="transform-existing-account-to-an-organization"></a>转换到组织的现有帐户

> [!Warning]
> 帐户转换是不可逆： 不能转换回用户帐户的组织。

如果要管理的包作为一个团队使用单个用户帐户并且想要将该帐户转换成组织，使用**转换您的帐户以组织**选项卡上**管理组织**页上：

![在 nuget.org 上的选项来转换到组织的现有帐户](media/org-transform-option.png)

在下一页上，指定不同的用户帐户分配为管理员的组织，然后选择**转换**。

![输入用于将转换到组织的用户帐户的信息](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理组织的成员

作为组织管理员，您可以通过提供每个成员的 nuget.org 中添加成员*用户帐户名*; 不能使用电子邮件地址。 您然后将标记每个成员作为协作者或管理员具有以下权限：

| 权限 | 协作者 | 管理员 |
| --- | --- | --- |
| 管理组织的包<br/>（提交新的包、 更新或取消列出现有的包） | 是 | 是 |
| 更改组织元数据<br/>（电子邮件，通知设置） | 否 | 是 |
| 管理组织的成员 | 否 | 是 |
| 请求或组织包的 co-ownership 请求处理 | 否 | 是 |

## <a name="managing-packages"></a>管理包

你的帐户和所有组织您的一个成员可以查看所有包[管理包](https://www.nuget.org/account/Packages)页。 若要查看特定于你的帐户或任何特定组织包，使用右上角的帐户筛选器页面右上角。

![使用帐户筛选器管理包](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>将包传输到组织
如果你想要将部分包传输到新创建的组织，就可以做到请求要共同拥有包的组织帐户，然后删除您自己作为所有者。 如果你是组织的管理员，则无需接受所有权确认。 但是，如果你是协作者，作为所有者添加组织需要一个管理员能够接受所有权。

## <a name="publishing-packages"></a>发布包

您需要将包发布到组织，如将包发布到用户帐户： 通过直接将包上传到 nuget.org 或通过将包推送`nuget push`或`dotnet nuget push`CLI 命令。

### <a name="uploading-packages"></a>上传包

当您将新的程序包直接上载上[nuget.org 上传](https://www.nuget.org/packages/manage/upload)页上，则包将所有者分配到用户或组织帐户：

![上传包帐户选项](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 密钥

若要将包推送`nuget push`或`dotnet nuget push`CLI 命令，必须获取 API 密钥所需的这些命令。 有关详细信息，请参阅[发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。

在创建新的 API 密钥，选择相应的组织中**包所有者**下拉列表。 在创建任何 API 密钥是仅适用于所选的组织：

![帐户选项的 API 密钥](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>删除组织

作为用户，您可以将自己删除组织中通过选择`X`按钮通过您的组织的成员身份所示：

![从组织中删除用户帐户](media/org-remove-self-option.png)

管理员可以从该组织，包括其他管理员删除任何成员。 如果您组织的唯一管理员，不能将自己删除，除非以管理员身份添加另一个成员。

### <a name="deleting-an-organization-account"></a>删除组织帐户

此功能即将推出。
