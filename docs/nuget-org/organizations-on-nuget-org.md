---
title: NuGet.org 上的组织
description: NuGet.org 上的组织可帮助你管理由组或在团队、公司环境中发布的包。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427072"
---
# <a name="your-organization-on-nugetorg"></a>NuGet.org 上的组织

组织使企业和开源项目能够使用单个 NuGet.org 标识在包上进行协作。 对于包使用者，组织帐户看起来与 NuGet.org 上的现有用户帐户相同。

## <a name="organization-accounts-vs-individual-accounts"></a>组织帐户与个人帐户

组织帐户具有一个或多个个人（用户）帐户作为其成员。 这些成员可以管理一组包，同时保持所有权的单一标识。

你的个人帐户是你在 NuGet.org 上的标识，可以是任意数量组织的成员。 包可以属于组织帐户，就像它可以属于个人帐户一样。 包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。

## <a name="adding-a-new-organization"></a>添加新组织

要添加新组织，请在 NuGet.org 上选择你的帐户，然后选择“管理组织...”菜单命令  ：

![NuGet.org 上用于管理员组织的菜单选项](media/org-manage-option.png)

在下一页上，选择“添加新组织”按钮  ：

![应用在 NuGet.org 上创建新组织的按钮](media/org-add-new-option.png)

在下一页上，提供组织名称和电子邮件地址。 由于组织帐户与用户帐户共用同一命名空间，因此组织名称必须不同于任何其他现有组织或用户帐户。 电子邮件地址在所有帐户中也必须是唯一的。

![在 NuGet.org 上添加新的组织页面](media/org-add-new-page.png)

创建组织帐户后，你就是管理员，可以为组织提交包并添加组织成员。

### <a name="transform-existing-account-to-an-organization"></a>将现有帐户转换为组织

> [!Warning]
> 帐户转换是不可逆转的：无法将组织转换回用户帐户。

如果以团队的形式使用一个用户帐户管理包并希望将该帐户转换为组织，请使用“管理组织”页上的“将你的帐户转换为组织”选项   ：

![NuGet.org 上的选项可将现有帐户转换为组织](media/org-transform-option.png)

在下一页上，指定其他用户帐户以分配作为组织管理员，然后选择“转换”  。

![输入用于将用户帐户转换为组织的信息](media/org-transform-page.png)

## <a name="managing-organization-members"></a>管理组织成员

组织管理员可以通过提供每个成员的 NuGet.org 用户帐户名来添加成员；不能使用电子邮件地址  。 然后将每个成员标记为具有以下权限的协作者或管理员：

| 权限 | 协作者 | 管理员 |
| --- | --- | --- |
| 管理组织的包<br/>（提交新包，更新或取消列出现有包） | 是 | 是 |
| 更改组织元数据<br/>（电子邮件地址、通知设置） | 否 | 是 |
| 管理组织成员 | 否 | 是 |
| 提出或处理组织包的共同所有权请求 | 否 | 是 |

## <a name="managing-packages"></a>管理包

在[管理包](https://www.nuget.org/account/Packages)页上可以跨你的帐户和你所属的组织查看所有包。 要查看特定于你的帐户或任何特定组织的包，请使用页面右上角的帐户筛选器。

![使用帐户筛选器管理包](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>将包转移到组织
如果希望将某些包转移到新创建的组织，可以通过请求组织帐户共同拥有该包，然后移除自己的所有者身份来实现。 如果你是组织的管理员，则无需确认即可接受所有权。 但如果你是协作者，则添加组织作为所有者需要其中一个管理员接受所有权。

## <a name="publishing-packages"></a>发布包

将包发布到组织的方法与将包发布到用户帐户的方法类似：直接将包上传到 NuGet.org，或者通过 `nuget push` 或 `dotnet nuget push` CLI 命令推送包。

### <a name="uploading-packages"></a>上传包

在 [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) 页上直接上传新包时，你会将包所有者分配给用户或组织帐户：

![使用帐户选项上传包](media/org-upload-option.png)

### <a name="using-api-keys"></a>使用 API 密钥

要通过 `nuget push` 或 `dotnet nuget push` CLI 命令推送包，必须获取这些命令所需的 API 密钥。 有关详细信息，请参阅[发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。

创建新的 API 密钥时，请在“包所有者”下拉列表中选择相应的组织  。 你创建的任何 API 密钥仅适用于所选组织：

![具有帐户选项的 API 密钥](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>移除组织

用户可以通过选择组织成员身份旁所示的“X”按钮将自己从组织中移除  ：

![从组织中移除用户帐户](media/org-remove-self-option.png)

管理员可以从组织中移除任何成员，包括其他管理员。 如果你是组织的唯一管理员，除非添加另一个成员作为管理员，否则无法移除自己。

### <a name="deleting-an-organization-account"></a>删除组织帐户

可以通过单击组织页面中显示的“删除”按钮来删除组织帐户  。

![删除组织](media/org-delete-option.png)

若要删除组织，则必须单击“删除组织”确认按钮进行确认  。
