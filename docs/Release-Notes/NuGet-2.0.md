---
title: "NuGet 2.0 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 2.0 的发行说明。"
keywords: "NuGet 2.0 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="229c7-104">NuGet 2.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="229c7-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="229c7-105">[NuGet 1.8 发行说明](../release-notes/nuget-1.8.md) | [NuGet 2.1 发行说明](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="229c7-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="229c7-106">NuGet 2.0 已于 2012 年 6 月 19 日发布。</span><span class="sxs-lookup"><span data-stu-id="229c7-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="229c7-107">已知的安装问题</span><span class="sxs-lookup"><span data-stu-id="229c7-107">Known Installation Issue</span></span>
<span data-ttu-id="229c7-108">如果你运行的 VS 2010 SP1，你可能尝试升级 NuGet，如果安装了较旧版本时遇到安装错误。</span><span class="sxs-lookup"><span data-stu-id="229c7-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="229c7-109">解决方法是只需卸载 NuGet，然后从 VS 扩展库安装它。</span><span class="sxs-lookup"><span data-stu-id="229c7-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="229c7-110">请参阅[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)有关详细信息，或[转到 VS 修补程序直接](http://bit.ly/vsixcertfix)。</span><span class="sxs-lookup"><span data-stu-id="229c7-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="229c7-111">注意： 如果 Visual Studio 不会使您可以卸载的扩展 （卸载按钮为禁用），然后你可能需要重新启动 Visual Studio 中使用"以管理员身份运行"。</span><span class="sxs-lookup"><span data-stu-id="229c7-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="229c7-112">包还原同意目前处于活动状态</span><span class="sxs-lookup"><span data-stu-id="229c7-112">Package restore consent is now active</span></span>

<span data-ttu-id="229c7-113">在此所述[将它发布在包还原同意](http://blog.nuget.org/20120518/package-restore-and-consent.html)，NuGet 2.0 现在将需要指定同意的情况下，以便启用程序包还原以联机并下载包。</span><span class="sxs-lookup"><span data-stu-id="229c7-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="229c7-114">请确保你提供通过包管理器配置对话框或 EnableNuGetPackageRestore 环境变量的同意。</span><span class="sxs-lookup"><span data-stu-id="229c7-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="229c7-115">由目标框架的组依赖项</span><span class="sxs-lookup"><span data-stu-id="229c7-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="229c7-116">依赖项而异的包从版本 2.0 开始，基于目标项目的框架配置文件。</span><span class="sxs-lookup"><span data-stu-id="229c7-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="229c7-117">这使用更新完成`.nuspec`架构。</span><span class="sxs-lookup"><span data-stu-id="229c7-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="229c7-118">`<dependencies>`元素现在可以包含一套`<group>`元素。</span><span class="sxs-lookup"><span data-stu-id="229c7-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="229c7-119">每个组包含零个或多`<dependency>`元素和`targetFramework`属性。</span><span class="sxs-lookup"><span data-stu-id="229c7-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="229c7-120">如果目标框架与目标项目框架配置文件兼容，位于组内的所有依赖项是一起安装。</span><span class="sxs-lookup"><span data-stu-id="229c7-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="229c7-121">例如: </span><span class="sxs-lookup"><span data-stu-id="229c7-121">For example:</span></span>

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

<span data-ttu-id="229c7-122">请注意，一个组可以包含**零**依赖关系。</span><span class="sxs-lookup"><span data-stu-id="229c7-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="229c7-123">在上面的示例中，如果包安装到的项目是面向 Silverlight 3.0 或更高版本，将安装没有依赖关系。</span><span class="sxs-lookup"><span data-stu-id="229c7-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="229c7-124">如果包安装到的项目是面向.NET 4.0 或更高版本，将安装 jQuery 和 WebActivator，两个依赖关系。</span><span class="sxs-lookup"><span data-stu-id="229c7-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="229c7-125">如果包安装到面向早期版本的这些 2 的框架或任何其他框架的项目后，将安装 RouteMagic 1.1.0。</span><span class="sxs-lookup"><span data-stu-id="229c7-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="229c7-126">组之间没有任何继承。</span><span class="sxs-lookup"><span data-stu-id="229c7-126">There is no inheritance between groups.</span></span> <span data-ttu-id="229c7-127">如果项目的目标框架与相匹配`targetFramework`将安装的一个组，只有该组内部依赖关系的属性。</span><span class="sxs-lookup"><span data-stu-id="229c7-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="229c7-128">包可以在两种格式之一指定包的依赖项： 的简单列表的旧格式`<dependency>`元素或组。</span><span class="sxs-lookup"><span data-stu-id="229c7-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="229c7-129">如果`<group>`格式时，不能将此包安装到早于 2.0 的 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="229c7-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="229c7-130">请注意不允许混合使用两种格式。</span><span class="sxs-lookup"><span data-stu-id="229c7-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="229c7-131">例如，下面的代码段是**无效**和将拒绝的 NuGet。</span><span class="sxs-lookup"><span data-stu-id="229c7-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="229c7-132">由目标 framework 分组内容文件和 PowerShell 脚本</span><span class="sxs-lookup"><span data-stu-id="229c7-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="229c7-133">程序集引用，除了内容文件和 PowerShell 脚本也可以由目标框架分组。</span><span class="sxs-lookup"><span data-stu-id="229c7-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="229c7-134">在中找到的相同文件夹结构`lib`用于指定目标框架的文件夹现在可将应用到相同的方式`content`和`tools`文件夹。</span><span class="sxs-lookup"><span data-stu-id="229c7-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="229c7-135">例如: </span><span class="sxs-lookup"><span data-stu-id="229c7-135">For example:</span></span>

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

<span data-ttu-id="229c7-136">**请注意**： 因为`init.ps1`解决方案级别执行且不依赖于任何单个项目，必须将它放置在直接`tools`文件夹。</span><span class="sxs-lookup"><span data-stu-id="229c7-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="229c7-137">如果放置在特定于框架的文件夹内，它将被忽略。</span><span class="sxs-lookup"><span data-stu-id="229c7-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="229c7-138">此外，NuGet 2.0 中的新功能是框架文件夹可以是*空*，在这种情况下，NuGet 将不添加程序集引用，将内容文件添加或运行特定的框架版本的 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="229c7-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="229c7-139">在示例中，文件夹`content\net40`为空。</span><span class="sxs-lookup"><span data-stu-id="229c7-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="229c7-140">改进的选项卡完成性能</span><span class="sxs-lookup"><span data-stu-id="229c7-140">Improved tab completion performance</span></span>
<span data-ttu-id="229c7-141">已更新 NuGet 包管理器控制台中的选项卡完成功能，从而显著改善性能。</span><span class="sxs-lookup"><span data-stu-id="229c7-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="229c7-142">将从按下 tab 键直到建议下拉列表中出现的时间少得多延迟。</span><span class="sxs-lookup"><span data-stu-id="229c7-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="229c7-143">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="229c7-143">Bug Fixes</span></span>
<span data-ttu-id="229c7-144">NuGet 2.0 包括许多主要侧重于包还原同意和性能的 bug 修补程序。</span><span class="sxs-lookup"><span data-stu-id="229c7-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="229c7-145">有关工作的完整列表项固定在 NuGet 2.0 中，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)。</span><span class="sxs-lookup"><span data-stu-id="229c7-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
