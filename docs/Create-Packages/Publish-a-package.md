---
title: 如何发布 NuGet 包 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 详细说明如何将 NuGet 包发布到 nuget.org 或专用源，以及如何在 nuget.org 上管理包所有权。
keywords: NuGet 包发布, 发布 NuGet 包, NuGet 包所有权, 发布到 nuget.org, NuGet 专用源
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="084db-104">发布包</span><span class="sxs-lookup"><span data-stu-id="084db-104">Publishing packages</span></span>

<span data-ttu-id="084db-105">创建程序包并获得 `.nukpg` 文件后，即可轻松以公开或私密方式将其提供给其他开发人员：</span><span class="sxs-lookup"><span data-stu-id="084db-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="084db-106">根据本文中的介绍，可通过 [nuget.org](https://www.nuget.org/packages/manage/upload) 将公共包全局提供给所有开发人员（需要 NuGet 4.1.0+）。</span><span class="sxs-lookup"><span data-stu-id="084db-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="084db-107">通过以下方式可以仅向团队或组织提供专用包：在文件共享、专用 NuGet 服务器、[Visual Studio Team Services 包管理](https://www.visualstudio.com/docs/package/nuget/publish)或第三方存储库（如 myget、ProGet、Nexus 存储库和 Artifactory）上承载专用包。</span><span class="sxs-lookup"><span data-stu-id="084db-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="084db-108">有关其他详细信息，请参阅[承载包概述](../hosting-packages/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="084db-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="084db-109">本文介绍如何发布到 nuget.org；有关发布到 Visual Studio Team Services 的信息，请参阅[包管理](https://www.visualstudio.com/docs/package/nuget/publish)。</span><span class="sxs-lookup"><span data-stu-id="084db-109">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="084db-110">发布到 nuget.org</span><span class="sxs-lookup"><span data-stu-id="084db-110">Publish to nuget.org</span></span>

<span data-ttu-id="084db-111">对于 nuget.org，必须使用 Microsoft 帐户进行登录，将需要在 nuget.org 中注册此帐户。此外可以使用较旧版本的门户创建的 nuget.org 帐户进行登录。</span><span class="sxs-lookup"><span data-stu-id="084db-111">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet 登录位置](media/publish_NuGetSignIn.png)

<span data-ttu-id="084db-113">接下来，可根据以下各节中的介绍，通过 nuget.org Web 门户上传包、从命令行（需要 `nuget.exe` 4.1.0+）将包推送到 nuget.org 或通过 Visual Studio Team Services 在 CI/CD 过程中发布包。</span><span class="sxs-lookup"><span data-stu-id="084db-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="084db-114">Web 门户：使用 nuget.org 上的“上传包”选项卡</span><span class="sxs-lookup"><span data-stu-id="084db-114">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="084db-115">选择 nuget.org 顶部菜单中的“上传”，并浏览到包位置。</span><span class="sxs-lookup"><span data-stu-id="084db-115">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![在 nuget.org 上上传包](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="084db-117">nuget.org 告知包名称是否可用。</span><span class="sxs-lookup"><span data-stu-id="084db-117">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="084db-118">如果无法使用，则更改项目中的包标识符、重新生成，并重试上传。</span><span class="sxs-lookup"><span data-stu-id="084db-118">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="084db-119">如果包名称可用，nuget.org 将打开“验证”部分，可以在其中查看包清单中的元数据。</span><span class="sxs-lookup"><span data-stu-id="084db-119">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="084db-120">若要更改任何元数据，请编辑项目（项目文件或 `.nuspec` 文件）、重新生成、重新创建包，然后再次上传。</span><span class="sxs-lookup"><span data-stu-id="084db-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="084db-121">在“导入文档”下，可以粘贴 Markdown、将 URL 指向文档，或上传文档文件。</span><span class="sxs-lookup"><span data-stu-id="084db-121">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="084db-122">当所有信息准备就绪后，选择“提交”按钮</span><span class="sxs-lookup"><span data-stu-id="084db-122">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="084db-123">命令行</span><span class="sxs-lookup"><span data-stu-id="084db-123">Command line</span></span>

<span data-ttu-id="084db-124">若要将包推送到 nuget.org，必须使用实现所需 [NuGet 协议](../api/nuget-protocols.md)的 [nuget.exe v4.1.0 或更高版本](https://www.nuget.org/downloads)。</span><span class="sxs-lookup"><span data-stu-id="084db-124">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="084db-125">还需要在 nuget.org 上创建的 API 密钥。</span><span class="sxs-lookup"><span data-stu-id="084db-125">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="084db-126">创建 API 密钥</span><span class="sxs-lookup"><span data-stu-id="084db-126">Create API keys</span></span>

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="084db-127">用 dotnet nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="084db-127">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="084db-128">用 nuget push 发布</span><span class="sxs-lookup"><span data-stu-id="084db-128">Publish with nuget push</span></span>

1. <span data-ttu-id="084db-129">在命令提示符处运行以下命令，将 `<your_API_key>` 替换为从 nuget.org 获取的密钥：</span><span class="sxs-lookup"><span data-stu-id="084db-129">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="084db-130">此命令将 API 密钥存储在 NuGet 配置中，以便需要在同一台计算机上再次重复此步骤。</span><span class="sxs-lookup"><span data-stu-id="084db-130">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="084db-131">使用以下命令将包推送到 NuGet 库：</span><span class="sxs-lookup"><span data-stu-id="084db-131">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="084db-132">包验证和编制索引</span><span class="sxs-lookup"><span data-stu-id="084db-132">Package validation and indexing</span></span>

<span data-ttu-id="084db-133">推送到 nuget.org 的包会进行多项验证，如病毒检查。</span><span class="sxs-lookup"><span data-stu-id="084db-133">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="084db-134">（定期扫描 nuget.org 上的所有包。）</span><span class="sxs-lookup"><span data-stu-id="084db-134">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="084db-135">.</span><span class="sxs-lookup"><span data-stu-id="084db-135">.</span></span> <span data-ttu-id="084db-136">包通过所有验证检查后，对包编制索引并将其显示在搜索结果中可能需要一些时间。</span><span class="sxs-lookup"><span data-stu-id="084db-136">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="084db-137">编制索引完成后，你会收到一封确认已成功发布包的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="084db-137">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="084db-138">如果包未通过验证检查，将更新包详细信息页面以显示相关错误，同时你也会收到包含相关通知的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="084db-138">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="084db-139">包验证和编制索引所需的时间通常不超过 15 分钟。</span><span class="sxs-lookup"><span data-stu-id="084db-139">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="084db-140">如果发布包所用时间超出预期，请访问 [status.nuget.org](https://status.nuget.org/) 检查 nuget.org 是否遇到任何中断。</span><span class="sxs-lookup"><span data-stu-id="084db-140">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="084db-141">如果所有系统均正常运行，但一个小时之内还未成功发布包，请登录 nuget.org 并使用包页面上的“联系支持人员”链接与我们联系。</span><span class="sxs-lookup"><span data-stu-id="084db-141">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="084db-142">若要查看包状态，请选择 nuget.org 上帐户名称下的“管理包”。完成验证时，会收到确认电子邮件。</span><span class="sxs-lookup"><span data-stu-id="084db-142">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="084db-143">请注意，对包编制索引并将其显示在搜索结果中供其他人查找可能需要一些时间。在此期间，包页面上会出现以下消息：</span><span class="sxs-lookup"><span data-stu-id="084db-143">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![指示尚未发布包的消息](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="084db-145">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="084db-145">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="084db-146">如果在持续集成/部署过程中使用 Visual Studio Team Services 将包推送到 nuget.org，必须在 NuGet 任务中使用 `nuget.exe` 4.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="084db-146">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="084db-147">要了解详细信息，请参阅 [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/)（在生成中使用最新 NuGet）（Microsoft DevOps 博客）。</span><span class="sxs-lookup"><span data-stu-id="084db-147">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="084db-148">在 nuget.org 上管理包所有者</span><span class="sxs-lookup"><span data-stu-id="084db-148">Managing package owners on nuget.org</span></span>

<span data-ttu-id="084db-149">尽管每个 NuGet 包的 `.nuspec` 文件定义了该包的创建者，但 nuget.org 库不使用该元数据定义所有权。</span><span class="sxs-lookup"><span data-stu-id="084db-149">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="084db-150">相反，nuget.org 将初始所有权分配给发布包的人员。</span><span class="sxs-lookup"><span data-stu-id="084db-150">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="084db-151">他们通常是通过 nuget.org UI 上传包的已登录用户，或其 API 密钥与 `nuget SetApiKey` 或 `nuget push` 配合使用的用户。</span><span class="sxs-lookup"><span data-stu-id="084db-151">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="084db-152">所有包所有者均拥有包的完全权限，包括添加和删除其他所有者以及发布更新。</span><span class="sxs-lookup"><span data-stu-id="084db-152">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="084db-153">要更改包的所有权，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="084db-153">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="084db-154">使用包的当前所有者的帐户登录 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="084db-154">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="084db-155">选择帐户名称，选择“管理包”，然后展开“已发布的包”。</span><span class="sxs-lookup"><span data-stu-id="084db-155">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="084db-156">选择要管理的包，然后在右侧选择“管理所有者”。</span><span class="sxs-lookup"><span data-stu-id="084db-156">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="084db-157">此时，你具有多个选择：</span><span class="sxs-lookup"><span data-stu-id="084db-157">From here you have several options:</span></span>

1. <span data-ttu-id="084db-158">删除“当前所有者”下列出的任何所有者。</span><span class="sxs-lookup"><span data-stu-id="084db-158">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="084db-159">在“添加所有者”下添加所有者，方法是通过输入其用户名和一条消息，然后选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="084db-159">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="084db-160">此操作会向该新共有者发送包含确认链接的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="084db-160">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="084db-161">确认后，此人拥有添加和删除所有者的完全权限。</span><span class="sxs-lookup"><span data-stu-id="084db-161">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="084db-162">（确认之前，“当前所有者”部分指示此人的状态为“待审批”。）</span><span class="sxs-lookup"><span data-stu-id="084db-162">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="084db-163">要转让所有权（如变更所有权或在错误的帐户下发布包时），请添加新所有者，他们确认所有权后，即可将你从列表中删除。</span><span class="sxs-lookup"><span data-stu-id="084db-163">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="084db-164">要将所有权分配给公司或组，请使用转发到适当团队成员的电子邮件别名创建 nuget.org 帐户。</span><span class="sxs-lookup"><span data-stu-id="084db-164">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="084db-165">例如，各种 Microsoft ASP.NET 包由 [microsoft](http://nuget.org/profiles/microsoft) 和 [aspnet](http://nuget.org/profiles/aspnet) 帐户共同拥有，这两个帐户就是此类别名。</span><span class="sxs-lookup"><span data-stu-id="084db-165">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="084db-166">恢复包的所有权</span><span class="sxs-lookup"><span data-stu-id="084db-166">Recovering package ownership</span></span>

<span data-ttu-id="084db-167">有时，包所有者可能不太活跃。</span><span class="sxs-lookup"><span data-stu-id="084db-167">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="084db-168">例如，原始所有者可能已离开生产该包的公司，nuget.org 凭据丢失，或库中的早期 bug 导致包不具有所有者。</span><span class="sxs-lookup"><span data-stu-id="084db-168">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="084db-169">如果你是包的合法所有者且需要重新获得所有权，请使用 nuget.org 上的[联系表单](https://www.nuget.org/policies/Contact)向 NuGet 团队解释相关情况。</span><span class="sxs-lookup"><span data-stu-id="084db-169">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="084db-170">然后，我们按照流程验证你对包的所有权，包括通过包的项目 URL、Twitter、电子邮件或其他方式尝试找出现有所有者。</span><span class="sxs-lookup"><span data-stu-id="084db-170">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="084db-171">但如果所有其他方式均失败，我们会向你发送成为所有者的邀请。</span><span class="sxs-lookup"><span data-stu-id="084db-171">But if all else fails, we can send you a new invite to become an owner.</span></span>
