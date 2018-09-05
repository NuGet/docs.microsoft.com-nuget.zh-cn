---
title: NuGet 1.8 发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 1.8 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546616"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="4cc6a-103">NuGet 1.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="4cc6a-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="4cc6a-104">[NuGet 1.7 发行说明](../release-notes/nuget-1.7.md) | [NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="4cc6a-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="4cc6a-105">NuGet 1.8 已于 2012 年 5 月 23 日发布。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="4cc6a-106">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="4cc6a-106">Known Installation Issue</span></span>
<span data-ttu-id="4cc6a-107">如果运行 VS 2010 SP1，你可能会遇到安装错误，尝试升级 NuGet，如果您有安装了旧版本时。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="4cc6a-108">解决方法是简单地卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="4cc6a-109">请参阅[ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019)有关详细信息，或[直接转到 VS 修补程序](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="4cc6a-110">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮被禁用），然后您可能需要重启 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="4cc6a-111">NuGet 1.8 兼容 Windows XP 发布的修补程序</span><span class="sxs-lookup"><span data-stu-id="4cc6a-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="4cc6a-112">NuGet 1.8 发布不久后，我们了解到 1.8 中的加密更改中断用户在 Windows XP 上。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="4cc6a-113">由于我们已发布，解决了此问题的修补程序。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="4cc6a-114">通过更新 NuGet 通过 Visual Studio 扩展库，你收到此修补程序。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="4cc6a-115">功能</span><span class="sxs-lookup"><span data-stu-id="4cc6a-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="4cc6a-116">对本地化资源的附属包</span><span class="sxs-lookup"><span data-stu-id="4cc6a-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="4cc6a-117">NuGet 1.8 现在支持创建不同的软件包类似于.NET Framework 的附属程序集功能的本地化资源的能力。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="4cc6a-118">附属包创建方式与任何其他 NuGet 包添加了几个约定相同：</span><span class="sxs-lookup"><span data-stu-id="4cc6a-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="4cc6a-119">附属包 ID 和文件名称应包含匹配的一个标准的后缀[区域性使用的.NET Framework 字符串](http://msdn.microsoft.com/goglobal/bb896001.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="4cc6a-120">在其`.nuspec`文件，附属包应定义一个语言元素，具有同一 ID 中使用的区域性字符串</span><span class="sxs-lookup"><span data-stu-id="4cc6a-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="4cc6a-121">附属包应定义中的依赖项及其`.nuspec`到其核心包，即只需具有相同 ID 去掉语言后缀的包文件。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="4cc6a-122">要成功安装的存储库中可用的核心包要求。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="4cc6a-123">若要使用的本地化资源安装包，开发人员会将本地化的包显式选择从存储库。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="4cc6a-124">目前，NuGet 库不提供任何类型的特殊处理方式为附属包。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![包管理器对话框使用本地化包](./media/dlg-w-loc-packs.png)

<span data-ttu-id="4cc6a-126">因为附属包列出了其核心包的依赖项，是拉取到 NuGet 包文件夹和安装附属和 core 包。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![与本地化包的包文件夹](./media/fldr-loc-packs.png)

<span data-ttu-id="4cc6a-128">此外，同时安装附属包，NuGet 还可以识别区域性的字符串命名约定，然后将本地化的资源程序集复制到核心包中的正确子文件夹，以便它可以由.NET Framework 中选取。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![复制的资源文件夹与核心包文件夹](./media/fldr-copied-loc.png)

<span data-ttu-id="4cc6a-130">一个需要注意的附属包的现有 bug 是 NuGet 不会复制到的本地化的资源`bin`网站项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="4cc6a-131">将 NuGet 的下一个版本中修复此问题。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="4cc6a-132">有关演示如何创建和使用附属包的完整示例，请参阅[ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample)。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="4cc6a-133">包还原同意</span><span class="sxs-lookup"><span data-stu-id="4cc6a-133">Package Restore Consent</span></span>
<span data-ttu-id="4cc6a-134">在 NuGet 1.8 我们形式放置支持包还原，以保护用户隐私的一个重要约束打下基础。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="4cc6a-135">此约束要求构建项目和使用包还原显式同意包还原的解决方案的开发人员现在可以联机从配置的包源下载包。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="4cc6a-136">有两种方法来提供此许可。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="4cc6a-137">第一个可在包管理器配置对话框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="4cc6a-138">此方法主要针对开发人员计算机。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-138">This method is primarily intended for developer machines.</span></span>

![包管理器配置对话框](./media/pr-consent-configdlg.png)

<span data-ttu-id="4cc6a-140">第二种方法是将环境变量"EnableNuGetPackageRestore"设置为值"true"。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="4cc6a-141">此方法适用于无人参与的计算机，如 CI 或生成服务器。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="4cc6a-142">现在，如上面所述，我们仅奠定了基础，此功能在 NuGet 1.8 中。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="4cc6a-143">实际上，这意味着，尽管我们已添加的所有逻辑以启用该功能，它当前未强制执行在此版本中。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="4cc6a-144">它将被启用，但是，在下一个版本的 NuGet，因此我们想要让你知道它越早越好，以便可以适当地配置您的环境并因此不会受到影响我们启动时强制执行许可约束。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="4cc6a-145">有关更多详细信息，请参阅[团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html)有关此功能。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="4cc6a-146">nuget.exe 性能改进</span><span class="sxs-lookup"><span data-stu-id="4cc6a-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="4cc6a-147">通过修改安装命令下载和并行安装包，NuGet 1.8 做出了巨大的性能改进 nuget.exe – 且可由扩展包还原。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="4cc6a-148">高级别测试显示 6 包安装到项目的性能提高的 35%NuGet 1.8 中。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="4cc6a-149">增加到 25 的包的数量显示大约 60%的性能提升。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4cc6a-150">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="4cc6a-150">Bug Fixes</span></span>
<span data-ttu-id="4cc6a-151">NuGet 1.8 包括的包管理器控制台和包还原工作流，这是很多 bug 修复，特别是因为它与包还原同意和集成的 Windows 8 Express。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="4cc6a-152">有关工作的完整列表项中已修复 NuGet 1.8，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="4cc6a-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
