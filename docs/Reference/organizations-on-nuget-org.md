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
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="6b704-103">在 nuget.org 上的组织</span><span class="sxs-lookup"><span data-stu-id="6b704-103">Organization on nuget.org</span></span>

<span data-ttu-id="6b704-104">组织启用企业和开放源代码项目，在使用单个 nuget.org 标识包中进行协作。</span><span class="sxs-lookup"><span data-stu-id="6b704-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="6b704-105">对于包使用者，组织帐户将显示与 nuget.org 上的现有用户帐户相同。</span><span class="sxs-lookup"><span data-stu-id="6b704-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="6b704-106">与组织帐户的用户帐户</span><span class="sxs-lookup"><span data-stu-id="6b704-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="6b704-107">你的用户帐户为你的身份在 nuget.org，可以为任意数量的组织的成员。</span><span class="sxs-lookup"><span data-stu-id="6b704-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="6b704-108">包可以属于像它可以属于一个用户帐户的组织帐户。</span><span class="sxs-lookup"><span data-stu-id="6b704-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="6b704-109">包使用者看不到的用户帐户或组织帐户之间存在任何差异： 这两项以包的形式出现`owners`。</span><span class="sxs-lookup"><span data-stu-id="6b704-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="6b704-110">组织帐户具有作为其成员的一个或多个用户帐户。</span><span class="sxs-lookup"><span data-stu-id="6b704-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="6b704-111">在保持所有权的单个身份的同时，这些成员可以管理一组包。</span><span class="sxs-lookup"><span data-stu-id="6b704-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="6b704-112">添加新的组织</span><span class="sxs-lookup"><span data-stu-id="6b704-112">Adding a new organization</span></span>

<span data-ttu-id="6b704-113">若要添加新的组织，选择你的帐户上 nuget.org，然后选择**管理组织...** 菜单命令：</span><span class="sxs-lookup"><span data-stu-id="6b704-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![对于管理器的组织在 nuget.org 上的菜单选项](media/org-manage-option.png)

<span data-ttu-id="6b704-115">在下一页上，选择**添加新的组织**按钮：</span><span class="sxs-lookup"><span data-stu-id="6b704-115">On the next page, select the **Add new organization** button:</span></span>

![若要创建新的组织在 nuget.org 上的按钮](media/org-add-new-option.png)

<span data-ttu-id="6b704-117">在下一页上，提供组织名称和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="6b704-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="6b704-118">因为组织帐户共享用户帐户相同的命名空间，必须从其他任何现有的组织或用户帐户不同的组织名称。</span><span class="sxs-lookup"><span data-stu-id="6b704-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="6b704-119">电子邮件地址必须也是唯一的所有帐户。</span><span class="sxs-lookup"><span data-stu-id="6b704-119">The email address must also be unique across all accounts.</span></span>

![在 nuget.org 上添加新的组织页](media/org-add-new-page.png)

<span data-ttu-id="6b704-121">组织帐户创建后，你是管理员和可以提交为组织的包并添加组织成员。</span><span class="sxs-lookup"><span data-stu-id="6b704-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="6b704-122">转换到组织的现有帐户</span><span class="sxs-lookup"><span data-stu-id="6b704-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="6b704-123">是不可逆的帐户转换： 无法转换回用户帐户的组织。</span><span class="sxs-lookup"><span data-stu-id="6b704-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="6b704-124">如果您要为团队使用单个用户帐户管理包，并且想要将该帐户转换为组织，使用**转换你的组织帐户**选项**管理组织**页：</span><span class="sxs-lookup"><span data-stu-id="6b704-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![在 nuget.org 上的选项将组织现有的帐户](media/org-transform-option.png)

<span data-ttu-id="6b704-126">在下一页上，指定不同的用户帐户分配为管理员的组织，然后选择**转换**。</span><span class="sxs-lookup"><span data-stu-id="6b704-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![输入用于转换到组织的用户帐户的信息](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="6b704-128">管理组织成员</span><span class="sxs-lookup"><span data-stu-id="6b704-128">Managing organization members</span></span>

<span data-ttu-id="6b704-129">作为组织管理员，您可以通过提供每个成员 nuget.org 中添加成员*用户帐户名*; 不能使用电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="6b704-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="6b704-130">然后，你将标记为协作者或具有以下权限的管理员每个成员：</span><span class="sxs-lookup"><span data-stu-id="6b704-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="6b704-131">权限</span><span class="sxs-lookup"><span data-stu-id="6b704-131">Permission</span></span> | <span data-ttu-id="6b704-132">协作者</span><span class="sxs-lookup"><span data-stu-id="6b704-132">Collaborator</span></span> | <span data-ttu-id="6b704-133">管理员</span><span class="sxs-lookup"><span data-stu-id="6b704-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b704-134">管理组织的包</span><span class="sxs-lookup"><span data-stu-id="6b704-134">Manage the organization's packages</span></span><br/><span data-ttu-id="6b704-135">（提交新的包、 更新或不列出现有包）</span><span class="sxs-lookup"><span data-stu-id="6b704-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="6b704-136">是</span><span class="sxs-lookup"><span data-stu-id="6b704-136">Yes</span></span> | <span data-ttu-id="6b704-137">是</span><span class="sxs-lookup"><span data-stu-id="6b704-137">Yes</span></span> |
| <span data-ttu-id="6b704-138">更改组织元数据</span><span class="sxs-lookup"><span data-stu-id="6b704-138">Change organization metadata</span></span><br/><span data-ttu-id="6b704-139">（电子邮件地址，通知设置）</span><span class="sxs-lookup"><span data-stu-id="6b704-139">(email address, notification settings)</span></span> | <span data-ttu-id="6b704-140">否</span><span class="sxs-lookup"><span data-stu-id="6b704-140">No</span></span> | <span data-ttu-id="6b704-141">是</span><span class="sxs-lookup"><span data-stu-id="6b704-141">Yes</span></span> |
| <span data-ttu-id="6b704-142">管理组织成员</span><span class="sxs-lookup"><span data-stu-id="6b704-142">Manage organization members</span></span> | <span data-ttu-id="6b704-143">否</span><span class="sxs-lookup"><span data-stu-id="6b704-143">No</span></span> | <span data-ttu-id="6b704-144">是</span><span class="sxs-lookup"><span data-stu-id="6b704-144">Yes</span></span> |
| <span data-ttu-id="6b704-145">请求或组织包 co-ownership 请求处理</span><span class="sxs-lookup"><span data-stu-id="6b704-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="6b704-146">否</span><span class="sxs-lookup"><span data-stu-id="6b704-146">No</span></span> | <span data-ttu-id="6b704-147">是</span><span class="sxs-lookup"><span data-stu-id="6b704-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="6b704-148">管理包</span><span class="sxs-lookup"><span data-stu-id="6b704-148">Managing packages</span></span>

<span data-ttu-id="6b704-149">你可以查看所有包在你的帐户和你其中是成员的所有组织[管理包](https://www.nuget.org/account/Packages)页。</span><span class="sxs-lookup"><span data-stu-id="6b704-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="6b704-150">若要查看特定于你的帐户或任何特定的组织的包，请使用帐户筛选器在顶部页面右上角。</span><span class="sxs-lookup"><span data-stu-id="6b704-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![与帐户筛选器的管理包](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="6b704-152">将包传输到组织</span><span class="sxs-lookup"><span data-stu-id="6b704-152">Transferring packages to an organization</span></span>
<span data-ttu-id="6b704-153">如果你想要将某些包传输到新创建的组织，则可以通过做到请求要共同拥有包的组织帐户，然后删除自己作为所有者。</span><span class="sxs-lookup"><span data-stu-id="6b704-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="6b704-154">如果你是组织的管理员，则无需接受所有权确认。</span><span class="sxs-lookup"><span data-stu-id="6b704-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="6b704-155">但是，如果你是协作者，作为所有者添加组织需要一个接受所有权的管理员。</span><span class="sxs-lookup"><span data-stu-id="6b704-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="6b704-156">发布包</span><span class="sxs-lookup"><span data-stu-id="6b704-156">Publishing packages</span></span>

<span data-ttu-id="6b704-157">你需要将包发布到组织，如将包发布到的用户帐户： 通过直接将包上载到 nuget.org 或通过将包推送`nuget push`或`dotnet nuget push`CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="6b704-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="6b704-158">正在上载包</span><span class="sxs-lookup"><span data-stu-id="6b704-158">Uploading packages</span></span>

<span data-ttu-id="6b704-159">当你将新的程序包直接上载上[nuget.org 上载](https://www.nuget.org/packages/manage/upload)页上，你为用户或组织帐户分配的包所有者：</span><span class="sxs-lookup"><span data-stu-id="6b704-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![上载包帐户选项](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="6b704-161">使用 API 密钥</span><span class="sxs-lookup"><span data-stu-id="6b704-161">Using API keys</span></span>

<span data-ttu-id="6b704-162">若要推送包`nuget push`或`dotnet nuget push`CLI 命令，你必须获取 API 密钥所需的这些命令。</span><span class="sxs-lookup"><span data-stu-id="6b704-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="6b704-163">有关详细信息，请参阅[发布包](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package)。</span><span class="sxs-lookup"><span data-stu-id="6b704-163">For details, see [Publish a package](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span></span>

<span data-ttu-id="6b704-164">在创建新的 API 密钥，选择相应的组织中**包所有者**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="6b704-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="6b704-165">你创建任何 API 密钥是仅适用于选组织：</span><span class="sxs-lookup"><span data-stu-id="6b704-165">Any API key you create is applicable only to the chosen organization:</span></span>

![使用帐户选项的 API 密钥](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="6b704-167">删除组织</span><span class="sxs-lookup"><span data-stu-id="6b704-167">Removing an organization</span></span>

<span data-ttu-id="6b704-168">作为用户，你可以删除自己的组织中通过选择`X`按钮的你的组织的成员资格所示：</span><span class="sxs-lookup"><span data-stu-id="6b704-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![从组织中删除用户帐户](media/org-remove-self-option.png)

<span data-ttu-id="6b704-170">管理员可以从组织，包括其他管理员删除任何成员。</span><span class="sxs-lookup"><span data-stu-id="6b704-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="6b704-171">如果你组织的唯一管理员，不能删除自己，除非以管理员身份添加其他成员。</span><span class="sxs-lookup"><span data-stu-id="6b704-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="6b704-172">删除组织帐户</span><span class="sxs-lookup"><span data-stu-id="6b704-172">Deleting an organization account</span></span>

<span data-ttu-id="6b704-173">此功能即将推出。</span><span class="sxs-lookup"><span data-stu-id="6b704-173">This feature is coming soon.</span></span>
