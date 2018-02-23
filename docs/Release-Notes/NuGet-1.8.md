---
title: "NuGet 1.8 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 1.8 的发行说明。"
keywords: "NuGet 1.8 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 139c30e29d8148eab7298329a07d8e412259e595
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="eebdb-104">NuGet 1.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="eebdb-104">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="eebdb-105">[NuGet 1.7 发行说明](../release-notes/nuget-1.7.md) | [NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="eebdb-105">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="eebdb-106">NuGet 1.8 已于 2012 年 5 月 23 日发布。</span><span class="sxs-lookup"><span data-stu-id="eebdb-106">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="eebdb-107">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="eebdb-107">Known Installation Issue</span></span>
<span data-ttu-id="eebdb-108">如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="eebdb-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="eebdb-109">解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="eebdb-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="eebdb-110">请参阅[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)有关详细信息，或[转到 VS 修补程序直接](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="eebdb-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="eebdb-111">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="eebdb-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="eebdb-112">NuGet 1.8 兼容 Windows XP 中，发布的修补程序</span><span class="sxs-lookup"><span data-stu-id="eebdb-112">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="eebdb-113">很快发布 NuGet 1.8 后，我们已了解 1.8 中的加密更改在 Windows XP 上中断用户。</span><span class="sxs-lookup"><span data-stu-id="eebdb-113">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="eebdb-114">由于我们已发布的修补程序来解决该问题。</span><span class="sxs-lookup"><span data-stu-id="eebdb-114">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="eebdb-115">通过更新 NuGet 通过 Visual Studio 扩展库，你将接收此修补程序。</span><span class="sxs-lookup"><span data-stu-id="eebdb-115">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="eebdb-116">功能</span><span class="sxs-lookup"><span data-stu-id="eebdb-116">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="eebdb-117">本地化资源的附属包</span><span class="sxs-lookup"><span data-stu-id="eebdb-117">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="eebdb-118">NuGet 1.8 现在支持创建单独的包的本地化资源，类似于.NET framework 的附属程序集功能的能力。</span><span class="sxs-lookup"><span data-stu-id="eebdb-118">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="eebdb-119">为通过添加少量的约定的任何其他 NuGet 包相同的方式创建一个附属包：</span><span class="sxs-lookup"><span data-stu-id="eebdb-119">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="eebdb-120">附属包 ID 和文件名称应包含匹配的标准之一后缀[区域性使用的.NET Framework 字符串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。</span><span class="sxs-lookup"><span data-stu-id="eebdb-120">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="eebdb-121">在其`.nuspec`文件，附属包应定义一个语言元素，具有相同 ID 中使用的区域性字符串</span><span class="sxs-lookup"><span data-stu-id="eebdb-121">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="eebdb-122">附属包应定义中的依赖项其`.nuspec`到其核心包中，只需具有相同 ID 的语言后缀减包文件。</span><span class="sxs-lookup"><span data-stu-id="eebdb-122">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="eebdb-123">要成功安装的存储库中可用的核心程序包要求。</span><span class="sxs-lookup"><span data-stu-id="eebdb-123">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="eebdb-124">若要安装包使用本地化的资源，开发人员显式选择的本地化的程序包从存储库。</span><span class="sxs-lookup"><span data-stu-id="eebdb-124">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="eebdb-125">目前，NuGet 库未提供任何类型的附属包的特殊处理。</span><span class="sxs-lookup"><span data-stu-id="eebdb-125">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![与本地化包的包管理器对话框](./media/dlg-w-loc-packs.png)

<span data-ttu-id="eebdb-127">由于附属包会列出对其核心包的依赖性，附属和核心包都已拉入 NuGet 包文件夹，并且安装。</span><span class="sxs-lookup"><span data-stu-id="eebdb-127">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![具有本地化包的包文件夹](./media/fldr-loc-packs.png)

<span data-ttu-id="eebdb-129">此外，时安装附属包，NuGet 还可识别的区域性字符串命名约定，然后将本地化的资源程序集复制到核心包内正确的子文件夹，以便它可以由.NET Framework 中选取。</span><span class="sxs-lookup"><span data-stu-id="eebdb-129">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![核心包文件夹与复制的资源文件夹](./media/fldr-copied-loc.png)

<span data-ttu-id="eebdb-131">一个现有的 bug，需要注意的附属包是 NuGet 不会复制到的本地化的资源`bin`适用于网站项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="eebdb-131">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="eebdb-132">将在下一个版本的 NuGet 中修复此问题。</span><span class="sxs-lookup"><span data-stu-id="eebdb-132">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="eebdb-133">有关演示如何创建和使用附属包的完整示例，请参阅[https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)。</span><span class="sxs-lookup"><span data-stu-id="eebdb-133">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="eebdb-134">包还原同意</span><span class="sxs-lookup"><span data-stu-id="eebdb-134">Package Restore Consent</span></span>
<span data-ttu-id="eebdb-135">在 NuGet 1.8，我们放置支持包还原，以保护用户个人信息的一个重要约束奠定基础。</span><span class="sxs-lookup"><span data-stu-id="eebdb-135">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="eebdb-136">此约束要求开发人员生成项目和使用程序包还原显式同意程序包还原的解决方案的联机从配置的包源中下载的程序包。</span><span class="sxs-lookup"><span data-stu-id="eebdb-136">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="eebdb-137">有两种方法提供此许可。</span><span class="sxs-lookup"><span data-stu-id="eebdb-137">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="eebdb-138">第一个可在包管理器配置对话框如下所示。</span><span class="sxs-lookup"><span data-stu-id="eebdb-138">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="eebdb-139">此方法主要用于开发人员计算机。</span><span class="sxs-lookup"><span data-stu-id="eebdb-139">This method is primarily intended for developer machines.</span></span>

![包管理器配置对话框](./media/pr-consent-configdlg.png)

<span data-ttu-id="eebdb-141">第二种方法是将环境变量"EnableNuGetPackageRestore"设置为"true"的值。</span><span class="sxs-lookup"><span data-stu-id="eebdb-141">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="eebdb-142">此方法适用于无人参与的计算机，如 CI 或生成服务器。</span><span class="sxs-lookup"><span data-stu-id="eebdb-142">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="eebdb-143">现在，如上面所述，我们仅具有在 NuGet 1.8 中排列此功能的基础工作。</span><span class="sxs-lookup"><span data-stu-id="eebdb-143">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="eebdb-144">实际上，这意味着，虽然我们已添加所有启用的功能的逻辑，但是它当前不强制执行在此版本中。</span><span class="sxs-lookup"><span data-stu-id="eebdb-144">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="eebdb-145">它将被启用，但是，在下一个版本的 NuGet，因此我们想要让你知道它越早越好，以便你可以相应地配置你的环境，并因此不会影响我们启动时强制实施同意约束。</span><span class="sxs-lookup"><span data-stu-id="eebdb-145">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="eebdb-146">有关更多详细信息，请参阅[团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)有关此功能。</span><span class="sxs-lookup"><span data-stu-id="eebdb-146">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="eebdb-147">nuget.exe 性能改进</span><span class="sxs-lookup"><span data-stu-id="eebdb-147">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="eebdb-148">通过修改将下载并在并行中安装包的安装命令，NuGet 1.8 会极大地提高性能 nuget.exe – 并且，通过扩展包还原。</span><span class="sxs-lookup"><span data-stu-id="eebdb-148">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="eebdb-149">高级别测试显示 6 包安装到项目的性能可以减少大约 35%NuGet 1.8 中。</span><span class="sxs-lookup"><span data-stu-id="eebdb-149">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="eebdb-150">增加到 25 的包数目显示大约 60%的性能有所提高。</span><span class="sxs-lookup"><span data-stu-id="eebdb-150">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="eebdb-151">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="eebdb-151">Bug Fixes</span></span>
<span data-ttu-id="eebdb-152">NuGet 1.8 包括相当多的 bug 修复，主要侧重于的包管理器控制台和包恢复工作流，尤其当它与包还原同意和 Windows 8 Express 集成。</span><span class="sxs-lookup"><span data-stu-id="eebdb-152">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="eebdb-153">有关工作的完整列表项固定在 NuGet 1.8，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="eebdb-153">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
