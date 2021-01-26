---
title: NuGet 2.0 发行说明
description: NuGet 2.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776985"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="4e8b5-103">NuGet 2.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="4e8b5-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="4e8b5-104">[NuGet 1.8 发行说明](../release-notes/nuget-1.8.md)  | [NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="4e8b5-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="4e8b5-105">NuGet 2.0 于2012年6月19日发布。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="4e8b5-106">已知安装问题</span><span class="sxs-lookup"><span data-stu-id="4e8b5-106">Known Installation Issue</span></span>
<span data-ttu-id="4e8b5-107">如果你运行的是 VS 2010 SP1，但如果你安装了较旧的版本，你可能会遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="4e8b5-108">解决方法是仅卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="4e8b5-109"><https://support.microsoft.com/kb/2581019>有关详细信息，请参阅，或[直接访问 VS 修补程序](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="4e8b5-110">注意：如果 Visual Studio 不允许卸载扩展 (禁用了 "卸载" 按钮) ，则可能需要使用 "以管理员身份运行" 重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="4e8b5-111">包还原许可现在处于活动状态</span><span class="sxs-lookup"><span data-stu-id="4e8b5-111">Package restore consent is now active</span></span>

<span data-ttu-id="4e8b5-112">如本 [文章在包还原许可](http://blog.nuget.org/20120518/package-restore-and-consent.html)中所述，NuGet 2.0 现在要求授予许可以使包还原联机并下载包。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="4e8b5-113">请确保已通过 "程序包管理器配置" 对话框或 EnableNuGetPackageRestore 环境变量提供同意。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="4e8b5-114">按目标框架对依赖项进行分组</span><span class="sxs-lookup"><span data-stu-id="4e8b5-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="4e8b5-115">从版本2.0 开始，根据目标项目的框架配置文件，包依赖项可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="4e8b5-116">这是使用已更新的架构来完成的 `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="4e8b5-117">`<dependencies>`元素现在可以包含一组 `<group>` 元素。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="4e8b5-118">每个组都包含零个或多个 `<dependency>` 元素和一个 `targetFramework` 属性。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="4e8b5-119">如果目标框架与目标项目框架配置文件兼容，则组中的所有依赖项都将一起安装。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="4e8b5-120">例如：</span><span class="sxs-lookup"><span data-stu-id="4e8b5-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="4e8b5-121">请注意，一个组可以包含 **零个** 依赖项。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="4e8b5-122">在上述示例中，如果将包安装到面向 Silverlight 3.0 或更高版本的项目中，则不会安装任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="4e8b5-123">如果将包安装到面向 .NET 4.0 或更高版本的项目中，将安装两个依赖项（jQuery 和 WebActivator）。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="4e8b5-124">如果将包安装到以这两个框架的早期版本为目标的项目或任何其他框架，将安装 RouteMagic 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="4e8b5-125">组之间没有继承。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-125">There is no inheritance between groups.</span></span> <span data-ttu-id="4e8b5-126">如果项目的目标框架与组的 `targetFramework` 属性匹配，则只会安装该组中的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="4e8b5-127">包可以使用以下两种格式中的一种来指定包依赖项：元素或组的简单列表的旧格式 `<dependency>` 。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="4e8b5-128">如果 `<group>` 使用格式，则包不能安装在版本早于2.0 的 NuGet 中。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="4e8b5-129">请注意，不允许混合使用这两种格式。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="4e8b5-130">例如，下面的代码段 **无效** 并将被 NuGet 拒绝。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="4e8b5-131">按目标框架对内容文件和 PowerShell 脚本进行分组</span><span class="sxs-lookup"><span data-stu-id="4e8b5-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="4e8b5-132">除程序集引用外，还可以按目标框架对内容文件和 PowerShell 脚本进行分组。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="4e8b5-133">现在，在用于指定目标框架的文件夹中找到的相同文件夹结构 `lib` 现在可以按与和文件夹相同的方式应用 `content` `tools` 。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="4e8b5-134">例如：</span><span class="sxs-lookup"><span data-stu-id="4e8b5-134">For example:</span></span>

```
\content
    \net11
        \MyContent.txt
    \net20
        \MyContent20.txt
    \net40
    \sl40
        \MySilverlightContent.html

\tools
    \init.ps1
    \net40
        \install.ps1
        \uninstall.ps1
    \sl40
        \install.ps1
        \uninstall.ps1
```

<span data-ttu-id="4e8b5-135">**注意**：由于 `init.ps1` 是在解决方案级别执行的，并且不依赖于任何单个项目，因此必须将其直接放置在 `tools` 文件夹下。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="4e8b5-136">如果放置在框架特定的文件夹中，则将被忽略。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="4e8b5-137">此外，NuGet 2.0 中的一项新功能是框架文件夹可以是 *空* 的，在这种情况下，NuGet 不会添加程序集引用、添加内容文件或针对特定的框架版本运行 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="4e8b5-138">在上面的示例中，该文件夹 `content\net40` 为空。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="4e8b5-139">改善了选项卡完成性能</span><span class="sxs-lookup"><span data-stu-id="4e8b5-139">Improved tab completion performance</span></span>
<span data-ttu-id="4e8b5-140">NuGet 包管理器控制台中的选项卡完成功能已更新，以显著提高性能。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="4e8b5-141">按下 tab 键时，延迟时间会大大减少，直到出现建议下拉列表。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4e8b5-142">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="4e8b5-142">Bug Fixes</span></span>
<span data-ttu-id="4e8b5-143">NuGet 2.0 包含多个 bug 修复，重点介绍包还原同意和性能。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="4e8b5-144">有关 NuGet 2.0 中已修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="4e8b5-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
