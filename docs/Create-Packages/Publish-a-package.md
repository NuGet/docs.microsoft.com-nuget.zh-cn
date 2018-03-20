---
title: "如何发布 NuGet 包 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "详细说明如何将 NuGet 包发布到 nuget.org 或专用源，以及如何在 nuget.org 上管理包所有权。"
keywords: "NuGet 包发布, 发布 NuGet 包, NuGet 包所有权, 发布到 nuget.org, NuGet 专用源"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6cb582c036392ae2792f2fa4d307370e91c4f961
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="324b6-104">发布包</span><span class="sxs-lookup"><span data-stu-id="324b6-104">Publishing packages</span></span>

<span data-ttu-id="324b6-105">创建程序包并获得 `.nukpg` 文件后，即可轻松以公开或私密方式将其提供给其他开发人员：</span><span class="sxs-lookup"><span data-stu-id="324b6-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="324b6-106">根据本主题中的介绍，可通过 [nuget.org](https://www.nuget.org/packages/manage/upload) 将公共包全局提供给所有开发人员。</span><span class="sxs-lookup"><span data-stu-id="324b6-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="324b6-107">通过以下方式可以仅向团队或组织提供专用包：在文件共享、专用 NuGet 服务器、[Visual Studio Team Services 包管理](https://www.visualstudio.com/docs/package/nuget/publish)或第三方存储库（如 myget、ProGet、Nexus 存储库和 Artifactory）上承载专用包。</span><span class="sxs-lookup"><span data-stu-id="324b6-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="324b6-108">有关其他详细信息，请参阅[承载包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="324b6-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="324b6-109">本主题介绍如何发布到 nuget.org；有关发布到 Visual Studio Team Services 的信息，请参阅[包管理](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="324b6-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="324b6-110">发布到 nuget.org</span><span class="sxs-lookup"><span data-stu-id="324b6-110">Publish to nuget.org</span></span>

<span data-ttu-id="324b6-111">对于 nuget.org，必须首先[注册一个免费帐户](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)或登录（如果已注册）：</span><span class="sxs-lookup"><span data-stu-id="324b6-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![NuGet 的注册和登录位置](media/publish_NuGetSignIn.png)

<span data-ttu-id="324b6-113">接下来，可根据以下各节中的介绍，通过 nuget.org Web 门户上传包、从命令行（需要 `nuget.exe` 4.1.0+）将包推送到 nuget.org 或通过 Visual Studio Team Services 在 CI/CD 过程中发布包。</span><span class="sxs-lookup"><span data-stu-id="324b6-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="324b6-114">Web 门户：使用 nuget.org 上的“上传包”选项卡</span><span class="sxs-lookup"><span data-stu-id="324b6-114">Web portal: use the Upload Package tab on nuget.org</span></span>

![使用 NuGet 包管理器上传包](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="324b6-116">命令行</span><span class="sxs-lookup"><span data-stu-id="324b6-116">Command line</span></span>

> [!Important]
> <span data-ttu-id="324b6-117">若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.1.0 或更高版本](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="324b6-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="324b6-118">单击用户名，导航到帐户设置。</span><span class="sxs-lookup"><span data-stu-id="324b6-118">Click on your user name to navigate to your account settings.</span></span>
1. <span data-ttu-id="324b6-119">在“API 密钥”下，单击“复制到剪贴板”，检索需要在 CLI 中使用的访问密钥：</span><span class="sxs-lookup"><span data-stu-id="324b6-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you need in the CLI:</span></span>

    ![从帐户设置中复制 API 密钥](media/publish_APIKey.png)

1. <span data-ttu-id="324b6-121">在命令提示符下，运行下列命令：</span><span class="sxs-lookup"><span data-stu-id="324b6-121">At a command prompt, run the following command:</span></span>

    ```cli
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="324b6-122">此命令会将 API 密钥存储在计算机上，因此无需在同一计算机上再次执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="324b6-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

1. <span data-ttu-id="324b6-123">使用以下命令将包推送到 NuGet 库：</span><span class="sxs-lookup"><span data-stu-id="324b6-123">Push your package to NuGet Gallery using the command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="324b6-124">在公布之前，上传到 nuget.org 的所有包都会扫描是否存在病毒，如果发现任何病毒，将拒绝包。</span><span class="sxs-lookup"><span data-stu-id="324b6-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="324b6-125">此外，还会定期扫描 nuget.org 上列出的所有包。</span><span class="sxs-lookup"><span data-stu-id="324b6-125">All packages listed on nuget.org are also scanned periodically.</span></span>

1. <span data-ttu-id="324b6-126">在 nuget.org 上的帐户中，单击“管理我的包”可查看刚刚发布的包；还会收到确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="324b6-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you also receive a confirmation email.</span></span> <span data-ttu-id="324b6-127">请注意，对包编制索引并将其显示在搜索结果中供其他人查找可能需要一些时间。在此期间，包页面上会出现以下消息：</span><span class="sxs-lookup"><span data-stu-id="324b6-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

    ![指示尚未对包编制索引的消息](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="324b6-129">包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="324b6-129">Package validation and indexing</span></span>

<span data-ttu-id="324b6-130">推送到 nuget.org 的包会进行多项验证。</span><span class="sxs-lookup"><span data-stu-id="324b6-130">Packages pushed to nuget.org undergo several validations.</span></span> <span data-ttu-id="324b6-131">包通过所有验证检查后，对包编制索引并将其显示在搜索结果中可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="324b6-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="324b6-132">编制索引完成后，你会收到一封确认已成功发布包的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="324b6-132">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="324b6-133">如果包未通过验证检查，将更新包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="324b6-133">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="324b6-134">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="324b6-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="324b6-135">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="324b6-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="324b6-136">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="324b6-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="324b6-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="324b6-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="324b6-138">如果在持续集成/部署过程中使用 Visual Studio Team Services 将包推送到 nuget.org，必须在 NuGet 任务中使用 `nuget.exe` 4.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="324b6-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="324b6-139">要了解详细信息，请参阅 [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)（在生成中使用最新 NuGet）（Microsoft DevOps 博客）。</span><span class="sxs-lookup"><span data-stu-id="324b6-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="324b6-140">在 nuget.org 上管理包所有者</span><span class="sxs-lookup"><span data-stu-id="324b6-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="324b6-141">尽管每个 NuGet 包的 `.nuspec` 文件定义了该包的创建者，但 nuget.org 库不使用该元数据定义所有权。</span><span class="sxs-lookup"><span data-stu-id="324b6-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="324b6-142">相反，nuget.org 将初始所有权分配给发布包的人员。</span><span class="sxs-lookup"><span data-stu-id="324b6-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="324b6-143">他们通常是通过 nuget.org UI 上传包的已登录用户，或其 API 密钥与 `nuget SetApiKey` 或 `nuget push` 配合使用的用户。</span><span class="sxs-lookup"><span data-stu-id="324b6-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="324b6-144">所有包所有者均拥有包的完全权限，包括添加和删除其他所有者以及发布更新。</span><span class="sxs-lookup"><span data-stu-id="324b6-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="324b6-145">要更改包的所有权，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="324b6-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="324b6-146">使用包的当前所有者的帐户登录 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="324b6-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="324b6-147">依次单击用户名和“管理我的包”，然后单击要管理的包。</span><span class="sxs-lookup"><span data-stu-id="324b6-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="324b6-148">单击左侧的“管理所有者”链接。</span><span class="sxs-lookup"><span data-stu-id="324b6-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="324b6-149">此时，你具有多个选择：</span><span class="sxs-lookup"><span data-stu-id="324b6-149">From here you have several options:</span></span>

1. <span data-ttu-id="324b6-150">要添加所有者，请输入其 NuGet 帐户名称，然后单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="324b6-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="324b6-151">此操作会向该新共有者发送包含确认链接的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="324b6-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="324b6-152">确认后，此人拥有添加和删除所有者的完全权限。</span><span class="sxs-lookup"><span data-stu-id="324b6-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="324b6-153">（确认之前，“管理所有者”页面指示此人的状态为“待审批”）。</span><span class="sxs-lookup"><span data-stu-id="324b6-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="324b6-154">要删除所有者，请在“管理所有者”上选择其名称，然后单击“删除”。</span><span class="sxs-lookup"><span data-stu-id="324b6-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="324b6-155">要转让所有权（如变更所有权或在错误的帐户下发布包时），只需添加新所有者，他们确认所有权后，即可将你从列表中删除。</span><span class="sxs-lookup"><span data-stu-id="324b6-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="324b6-156">要将所有权分配给公司或组，请使用转发到适当团队成员的电子邮件别名创建 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="324b6-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="324b6-157">例如，各种 Microsoft ASP.NET 包由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帐户共同拥有，这两个帐户就是此类别名。</span><span class="sxs-lookup"><span data-stu-id="324b6-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="324b6-158">恢复包的所有权</span><span class="sxs-lookup"><span data-stu-id="324b6-158">Recovering package ownership</span></span>

<span data-ttu-id="324b6-159">有时，包所有者可能不太活跃。</span><span class="sxs-lookup"><span data-stu-id="324b6-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="324b6-160">例如，原始所有者可能已离开生产该包的公司，nuget.org 凭据丢失，或库中的早期 bug 导致包不具有所有者。</span><span class="sxs-lookup"><span data-stu-id="324b6-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="324b6-161">如果你是包的合法所有者且需要重新获得所有权，请使用 nuget.org 上的[联系表单](https://www.nuget.org/policies/Contact)向 NuGet 团队解释相关情况。</span><span class="sxs-lookup"><span data-stu-id="324b6-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="324b6-162">然后，我们按照流程验证你对包的所有权，包括通过包的项目 URL、Twitter、电子邮件或其他方式尝试找出现有所有者。</span><span class="sxs-lookup"><span data-stu-id="324b6-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="324b6-163">但如果所有其他方式均失败，我们会向你发送成为所有者的邀请。</span><span class="sxs-lookup"><span data-stu-id="324b6-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
