---
title: NuGet 1.8 发行说明
description: NuGet 1.8 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8dd0fff88424c516d8b894412d07dcc53af19265
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777112"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="ab3fa-103">NuGet 1.8 发行说明</span><span class="sxs-lookup"><span data-stu-id="ab3fa-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="ab3fa-104">[NuGet 1.7 发行说明](../release-notes/nuget-1.7.md)  | [NuGet 2.0 发行说明](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="ab3fa-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="ab3fa-105">NuGet 1.8 于年5月 23 2012 日发布。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ab3fa-106">已知安装问题</span><span class="sxs-lookup"><span data-stu-id="ab3fa-106">Known Installation Issue</span></span>
<span data-ttu-id="ab3fa-107">如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ab3fa-108">解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ab3fa-109"><https://support.microsoft.com/kb/2581019>有关详细信息，请参阅，或[直接访问 VS 修补程序](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="ab3fa-110">注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="ab3fa-111">NuGet 1.8 与 Windows XP 兼容，已发布修补程序</span><span class="sxs-lookup"><span data-stu-id="ab3fa-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="ab3fa-112">在 NuGet 1.8 发布之后不久，我们已了解到1.8 中的密码更改在 Windows XP 上中断了用户。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="ab3fa-113">我们已经发布了解决此问题的修补程序。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="ab3fa-114">通过在 Visual Studio 扩展库中更新 NuGet，你会收到此修补程序。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="ab3fa-115">功能</span><span class="sxs-lookup"><span data-stu-id="ab3fa-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="ab3fa-116">本地化资源的附属包</span><span class="sxs-lookup"><span data-stu-id="ab3fa-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="ab3fa-117">NuGet 1.8 现在支持为本地化资源创建单独包的功能，类似于 .NET Framework 的附属程序集功能。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="ab3fa-118">附属包的创建方式与任何其他 NuGet 包相同，只是添加了一些约定：</span><span class="sxs-lookup"><span data-stu-id="ab3fa-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="ab3fa-119">附属包 ID 和文件名应包含与 [.NET Framework 使用的标准区域性字符串](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)之一匹配的后缀。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).</span></span>
* <span data-ttu-id="ab3fa-120">在其 `.nuspec` 文件中，附属包应定义一个语言元素，该元素具有在 ID 中使用的相同区域性字符串</span><span class="sxs-lookup"><span data-stu-id="ab3fa-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="ab3fa-121">附属包应将其文件中的依赖项定义 `.nuspec` 为其核心包，这只是 ID 与语言后缀相同的包。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="ab3fa-122">核心包需要在存储库中可用，才能成功安装。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="ab3fa-123">若要安装包含本地化资源的包，开发人员需要从存储库中显式选择本地化包。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="ab3fa-124">目前，NuGet 库不会向附属包提供任何类型的特殊处理。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![带有本地化包的包管理器对话框](./media/dlg-w-loc-packs.png)

<span data-ttu-id="ab3fa-126">由于附属包列出了其核心包的依赖项，因此附属包和核心包都将提取到 NuGet 包文件夹中并安装。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![带有本地化包的包文件夹](./media/fldr-loc-packs.png)

<span data-ttu-id="ab3fa-128">此外，在安装附属包时，NuGet 还识别区域性字符串命名约定，然后将本地化的资源程序集复制到核心包内的正确子文件夹中，以便 .NET Framework 可以对其进行选取。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![包含已复制资源文件夹的核心包文件夹](./media/fldr-copied-loc.png)

<span data-ttu-id="ab3fa-130">附属包需要注意的一个现有 bug 是 NuGet 不会将已本地化的资源复制到 `bin` 网站项目的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="ab3fa-131">此问题将在 NuGet 的下一版本中得到解决。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="ab3fa-132">有关演示如何创建和使用附属包的完整示例，请参阅 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) 。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="ab3fa-133">包还原许可</span><span class="sxs-lookup"><span data-stu-id="ab3fa-133">Package Restore Consent</span></span>
<span data-ttu-id="ab3fa-134">在 NuGet 1.8 中，我们为支持包还原中的重要约束设定了基础，以保护用户隐私。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="ab3fa-135">此约束要求开发人员生成项目和解决方案，这些项目和解决方案使用包还原来显式同意包还原的联机状态，以便从配置的包源下载包。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="ab3fa-136">有两种方法可提供此许可。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="ab3fa-137">第一个可以在 "包管理器配置" 对话框中找到，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="ab3fa-138">此方法主要用于开发人员计算机。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-138">This method is primarily intended for developer machines.</span></span>

![程序包管理器配置对话框](./media/pr-consent-configdlg.png)

<span data-ttu-id="ab3fa-140">第二种方法是将环境变量 "EnableNuGetPackageRestore" 设置为值 "true"。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="ab3fa-141">此方法适用于无人参与的计算机，例如 CI 或生成服务器。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="ab3fa-142">现在，如上所述，我们只在 NuGet 1.8 中为此功能奠定了基础。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="ab3fa-143">实际上，这意味着虽然我们添加了所有逻辑来启用此功能，但当前未在此版本中强制执行此功能。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="ab3fa-144">但在 NuGet 的下一版本中会启用此功能，因此，我们希望你尽快了解该功能，以便你可以适当地配置环境，从而在我们开始强制许可约束时不会受到影响。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="ab3fa-145">有关更多详细信息，请参阅 [团队博客文章](http://blog.nuget.org/20120518/package-restore-and-consent.html) 此功能。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="ab3fa-146">nuget.exe 性能改进</span><span class="sxs-lookup"><span data-stu-id="ab3fa-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="ab3fa-147">通过修改安装命令以并行下载和安装包，NuGet 1.8 使 nuget.exe 的性能和扩展包还原的性能得到显著提高。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="ab3fa-148">高级别测试表明，将6个包安装到项目中的性能将在 NuGet 1.8 中提高大约35%。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="ab3fa-149">将包数增加到25会显示大约60% 的性能提升。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ab3fa-150">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="ab3fa-150">Bug Fixes</span></span>
<span data-ttu-id="ab3fa-151">NuGet 1.8 包含非常多的 bug 修复，其中重点介绍了包管理器控制台和包还原工作流，尤其是在它与包还原许可和 Windows 8 Express 集成相关时。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="ab3fa-152">有关 NuGet 1.8 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="ab3fa-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>