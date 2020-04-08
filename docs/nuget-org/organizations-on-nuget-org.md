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
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="ccf86-103">NuGet.org 上的组织</span><span class="sxs-lookup"><span data-stu-id="ccf86-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="ccf86-104">组织使企业和开源项目能够使用单个 NuGet.org 标识在包上进行协作。</span><span class="sxs-lookup"><span data-stu-id="ccf86-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="ccf86-105">对于包使用者，组织帐户看起来与 NuGet.org 上的现有用户帐户相同。</span><span class="sxs-lookup"><span data-stu-id="ccf86-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="ccf86-106">组织帐户与个人帐户</span><span class="sxs-lookup"><span data-stu-id="ccf86-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="ccf86-107">组织帐户具有一个或多个个人（用户）帐户作为其成员。</span><span class="sxs-lookup"><span data-stu-id="ccf86-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="ccf86-108">这些成员可以管理一组包，同时保持所有权的单一标识。</span><span class="sxs-lookup"><span data-stu-id="ccf86-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="ccf86-109">你的个人帐户是你在 NuGet.org 上的标识，可以是任意数量组织的成员。</span><span class="sxs-lookup"><span data-stu-id="ccf86-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="ccf86-110">包可以属于组织帐户，就像它可以属于个人帐户一样。</span><span class="sxs-lookup"><span data-stu-id="ccf86-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="ccf86-111">包使用者看不到个人帐户或组织帐户之间的任何差异：两者都显示为包 `owners`。</span><span class="sxs-lookup"><span data-stu-id="ccf86-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="ccf86-112">添加新组织</span><span class="sxs-lookup"><span data-stu-id="ccf86-112">Adding a new organization</span></span>

<span data-ttu-id="ccf86-113">要添加新组织，请在 NuGet.org 上选择你的帐户，然后选择“管理组织...”菜单命令  ：</span><span class="sxs-lookup"><span data-stu-id="ccf86-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![NuGet.org 上用于管理员组织的菜单选项](media/org-manage-option.png)

<span data-ttu-id="ccf86-115">在下一页上，选择“添加新组织”按钮  ：</span><span class="sxs-lookup"><span data-stu-id="ccf86-115">On the next page, select the **Add new organization** button:</span></span>

![应用在 NuGet.org 上创建新组织的按钮](media/org-add-new-option.png)

<span data-ttu-id="ccf86-117">在下一页上，提供组织名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="ccf86-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="ccf86-118">由于组织帐户与用户帐户共用同一命名空间，因此组织名称必须不同于任何其他现有组织或用户帐户。</span><span class="sxs-lookup"><span data-stu-id="ccf86-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="ccf86-119">电子邮件地址在所有帐户中也必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ccf86-119">The email address must also be unique across all accounts.</span></span>

![在 NuGet.org 上添加新的组织页面](media/org-add-new-page.png)

<span data-ttu-id="ccf86-121">创建组织帐户后，你就是管理员，可以为组织提交包并添加组织成员。</span><span class="sxs-lookup"><span data-stu-id="ccf86-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="ccf86-122">将现有帐户转换为组织</span><span class="sxs-lookup"><span data-stu-id="ccf86-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="ccf86-123">帐户转换是不可逆转的：无法将组织转换回用户帐户。</span><span class="sxs-lookup"><span data-stu-id="ccf86-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="ccf86-124">如果以团队的形式使用一个用户帐户管理包并希望将该帐户转换为组织，请使用“管理组织”页上的“将你的帐户转换为组织”选项   ：</span><span class="sxs-lookup"><span data-stu-id="ccf86-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![NuGet.org 上的选项可将现有帐户转换为组织](media/org-transform-option.png)

<span data-ttu-id="ccf86-126">在下一页上，指定其他用户帐户以分配作为组织管理员，然后选择“转换”  。</span><span class="sxs-lookup"><span data-stu-id="ccf86-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![输入用于将用户帐户转换为组织的信息](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="ccf86-128">管理组织成员</span><span class="sxs-lookup"><span data-stu-id="ccf86-128">Managing organization members</span></span>

<span data-ttu-id="ccf86-129">组织管理员可以通过提供每个成员的 NuGet.org 用户帐户名来添加成员；不能使用电子邮件地址  。</span><span class="sxs-lookup"><span data-stu-id="ccf86-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="ccf86-130">然后将每个成员标记为具有以下权限的协作者或管理员：</span><span class="sxs-lookup"><span data-stu-id="ccf86-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="ccf86-131">权限</span><span class="sxs-lookup"><span data-stu-id="ccf86-131">Permission</span></span> | <span data-ttu-id="ccf86-132">协作者</span><span class="sxs-lookup"><span data-stu-id="ccf86-132">Collaborator</span></span> | <span data-ttu-id="ccf86-133">管理员</span><span class="sxs-lookup"><span data-stu-id="ccf86-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccf86-134">管理组织的包</span><span class="sxs-lookup"><span data-stu-id="ccf86-134">Manage the organization's packages</span></span><br/><span data-ttu-id="ccf86-135">（提交新包，更新或取消列出现有包）</span><span class="sxs-lookup"><span data-stu-id="ccf86-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="ccf86-136">是</span><span class="sxs-lookup"><span data-stu-id="ccf86-136">Yes</span></span> | <span data-ttu-id="ccf86-137">是</span><span class="sxs-lookup"><span data-stu-id="ccf86-137">Yes</span></span> |
| <span data-ttu-id="ccf86-138">更改组织元数据</span><span class="sxs-lookup"><span data-stu-id="ccf86-138">Change organization metadata</span></span><br/><span data-ttu-id="ccf86-139">（电子邮件地址、通知设置）</span><span class="sxs-lookup"><span data-stu-id="ccf86-139">(email address, notification settings)</span></span> | <span data-ttu-id="ccf86-140">否</span><span class="sxs-lookup"><span data-stu-id="ccf86-140">No</span></span> | <span data-ttu-id="ccf86-141">是</span><span class="sxs-lookup"><span data-stu-id="ccf86-141">Yes</span></span> |
| <span data-ttu-id="ccf86-142">管理组织成员</span><span class="sxs-lookup"><span data-stu-id="ccf86-142">Manage organization members</span></span> | <span data-ttu-id="ccf86-143">否</span><span class="sxs-lookup"><span data-stu-id="ccf86-143">No</span></span> | <span data-ttu-id="ccf86-144">是</span><span class="sxs-lookup"><span data-stu-id="ccf86-144">Yes</span></span> |
| <span data-ttu-id="ccf86-145">提出或处理组织包的共同所有权请求</span><span class="sxs-lookup"><span data-stu-id="ccf86-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="ccf86-146">否</span><span class="sxs-lookup"><span data-stu-id="ccf86-146">No</span></span> | <span data-ttu-id="ccf86-147">是</span><span class="sxs-lookup"><span data-stu-id="ccf86-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="ccf86-148">管理包</span><span class="sxs-lookup"><span data-stu-id="ccf86-148">Managing packages</span></span>

<span data-ttu-id="ccf86-149">在[管理包](https://www.nuget.org/account/Packages)页上可以跨你的帐户和你所属的组织查看所有包。</span><span class="sxs-lookup"><span data-stu-id="ccf86-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="ccf86-150">要查看特定于你的帐户或任何特定组织的包，请使用页面右上角的帐户筛选器。</span><span class="sxs-lookup"><span data-stu-id="ccf86-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![使用帐户筛选器管理包](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="ccf86-152">将包转移到组织</span><span class="sxs-lookup"><span data-stu-id="ccf86-152">Transferring packages to an organization</span></span>
<span data-ttu-id="ccf86-153">如果希望将某些包转移到新创建的组织，可以通过请求组织帐户共同拥有该包，然后移除自己的所有者身份来实现。</span><span class="sxs-lookup"><span data-stu-id="ccf86-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="ccf86-154">如果你是组织的管理员，则无需确认即可接受所有权。</span><span class="sxs-lookup"><span data-stu-id="ccf86-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="ccf86-155">但如果你是协作者，则添加组织作为所有者需要其中一个管理员接受所有权。</span><span class="sxs-lookup"><span data-stu-id="ccf86-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="ccf86-156">发布包</span><span class="sxs-lookup"><span data-stu-id="ccf86-156">Publishing packages</span></span>

<span data-ttu-id="ccf86-157">将包发布到组织的方法与将包发布到用户帐户的方法类似：直接将包上传到 NuGet.org，或者通过 `nuget push` 或 `dotnet nuget push` CLI 命令推送包。</span><span class="sxs-lookup"><span data-stu-id="ccf86-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="ccf86-158">上传包</span><span class="sxs-lookup"><span data-stu-id="ccf86-158">Uploading packages</span></span>

<span data-ttu-id="ccf86-159">在 [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) 页上直接上传新包时，你会将包所有者分配给用户或组织帐户：</span><span class="sxs-lookup"><span data-stu-id="ccf86-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![使用帐户选项上传包](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="ccf86-161">使用 API 密钥</span><span class="sxs-lookup"><span data-stu-id="ccf86-161">Using API keys</span></span>

<span data-ttu-id="ccf86-162">要通过 `nuget push` 或 `dotnet nuget push` CLI 命令推送包，必须获取这些命令所需的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="ccf86-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="ccf86-163">有关详细信息，请参阅[发布包](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)。</span><span class="sxs-lookup"><span data-stu-id="ccf86-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="ccf86-164">创建新的 API 密钥时，请在“包所有者”下拉列表中选择相应的组织  。</span><span class="sxs-lookup"><span data-stu-id="ccf86-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="ccf86-165">你创建的任何 API 密钥仅适用于所选组织：</span><span class="sxs-lookup"><span data-stu-id="ccf86-165">Any API key you create is applicable only to the chosen organization:</span></span>

![具有帐户选项的 API 密钥](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="ccf86-167">移除组织</span><span class="sxs-lookup"><span data-stu-id="ccf86-167">Removing an organization</span></span>

<span data-ttu-id="ccf86-168">用户可以通过选择组织成员身份旁所示的“X”按钮将自己从组织中移除  ：</span><span class="sxs-lookup"><span data-stu-id="ccf86-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![从组织中移除用户帐户](media/org-remove-self-option.png)

<span data-ttu-id="ccf86-170">管理员可以从组织中移除任何成员，包括其他管理员。</span><span class="sxs-lookup"><span data-stu-id="ccf86-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="ccf86-171">如果你是组织的唯一管理员，除非添加另一个成员作为管理员，否则无法移除自己。</span><span class="sxs-lookup"><span data-stu-id="ccf86-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="ccf86-172">删除组织帐户</span><span class="sxs-lookup"><span data-stu-id="ccf86-172">Deleting an organization account</span></span>

<span data-ttu-id="ccf86-173">可以通过单击组织页面中显示的“删除”按钮来删除组织帐户  。</span><span class="sxs-lookup"><span data-stu-id="ccf86-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![删除组织](media/org-delete-option.png)

<span data-ttu-id="ccf86-175">若要删除组织，则必须单击“删除组织”确认按钮进行确认  。</span><span class="sxs-lookup"><span data-stu-id="ccf86-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
