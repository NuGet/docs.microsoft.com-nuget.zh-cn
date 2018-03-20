---
title: "NuGet 程序包还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。"
keywords: "NuGet 包还原, NuGet 包安装, 安装包, 还原包, 依赖项版本, 禁用自动还原, 约束包版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a><span data-ttu-id="6deb1-104">包还原</span><span class="sxs-lookup"><span data-stu-id="6deb1-104">Package Restore</span></span>

<span data-ttu-id="6deb1-105">为了提升为更干净的开发环境并减少存储库大小，NuGet“包还原”在生成项目前会安装所有引用的包。</span><span class="sxs-lookup"><span data-stu-id="6deb1-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="6deb1-106">这种广泛使用的功能&mdash;是在 Visual Studio、.NET Core 2.0+ 和 Mono 上的 xbuild 中提供的&mdash;确保了所有依赖项在项目中均可用，无需那些包存储在源代码管理中（有关如何配置存储库排除包二进制文件的信息，请参阅[包与源代码管理](../consume-packages/packages-and-source-control.md)）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="6deb1-107">另外，还可以随时手动还原包。</span><span class="sxs-lookup"><span data-stu-id="6deb1-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="6deb1-108">有关生成服务器上的包还原的其他详细信息，请参阅[使用 TFBuild 还原包](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="6deb1-109">包还原概述</span><span class="sxs-lookup"><span data-stu-id="6deb1-109">Package restore overview</span></span>

<span data-ttu-id="6deb1-110">要还原包，首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="6deb1-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="6deb1-111">如果尚未安装程序包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-nuget-cache.md)中检索它。</span><span class="sxs-lookup"><span data-stu-id="6deb1-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="6deb1-112">如果在缓存中未找到包，则 NuGet 将尝试从所有已启用的源下载（和缓存）该包（请参阅[配置 NuGet 行为](Configuring-NuGet-Behavior.md)）；源也会出现在 Visual Studio 的“工具”>“选项”>“NuGet 包管理器”>“包源”列表中。</span><span class="sxs-lookup"><span data-stu-id="6deb1-112">If the package is not in the cache, NuGet then attempts to download (and cache) the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md)); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="6deb1-113">NuGet 会忽略包源的顺序，使用来自任何首先响应请求的源的包。</span><span class="sxs-lookup"><span data-stu-id="6deb1-113">NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="6deb1-114">在检查完所有源之前，NuGet 不会指示包还原失败。</span><span class="sxs-lookup"><span data-stu-id="6deb1-114">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="6deb1-115">届时，NuGet 仅会报告列表中最后一个源的失败。</span><span class="sxs-lookup"><span data-stu-id="6deb1-115">At that time, NuGet reports the failure for only the last source in the list.</span></span> <span data-ttu-id="6deb1-116">该错误说明包已不在其他任意源上，尽管那些源中的任何一个都没有单独显示错误。</span><span class="sxs-lookup"><span data-stu-id="6deb1-116">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="6deb1-117">包还原是通过以下方式触发的：</span><span class="sxs-lookup"><span data-stu-id="6deb1-117">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="6deb1-118">**dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-118">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="6deb1-119">使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。</span><span class="sxs-lookup"><span data-stu-id="6deb1-119">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="6deb1-120">**程序包管理器 UI（Windows 上的 Visual Studio）**：从模板创建项目以及构建项目时自动还原包（根据[启用和禁用包还原](#enabling-and-disabling-package-restore)中所述的选项）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-120">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="6deb1-121">此外，在 NuGet 4.0+ 中，对基于 .NET Core SDK 的项目进行更改时还会自动进行还原。</span><span class="sxs-lookup"><span data-stu-id="6deb1-121">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="6deb1-122">要手动还原，请右键单击“解决方案资源管理器”中的解决方案，选择“还原 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="6deb1-122">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="6deb1-123">如果一个或多个独立包仍未正确安装（即“解决方案资源管理器”显示错误图标），请使用程序包管理器 UI 卸载受影响的包并重新安装。</span><span class="sxs-lookup"><span data-stu-id="6deb1-123">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="6deb1-124">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="6deb1-124">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="6deb1-125">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则按照[启用和禁用包还原](#enabling-and-disabling-package-restore)中的以下说明打开自动还原。</span><span class="sxs-lookup"><span data-stu-id="6deb1-125">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="6deb1-126">**NuGet CLI**：使用 [nuget restore](../tools/cli-ref-restore.md) 命令还原项目文件（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）或 [packages.config](../reference/packages-config.md) 文件中列出的包。</span><span class="sxs-lookup"><span data-stu-id="6deb1-126">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)) or in a [packages.config](../reference/packages-config.md) file.</span></span> <span data-ttu-id="6deb1-127">此外，你还可以指定解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="6deb1-127">You can also specify a solution file.</span></span>

- <span data-ttu-id="6deb1-128">**MSBuild**：使用 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-128">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="6deb1-129">仅适用于 Visual Studio 2017 附带的 NuGet 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="6deb1-129">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="6deb1-130">`nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。</span><span class="sxs-lookup"><span data-stu-id="6deb1-130">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="6deb1-131">**Visual Studio Team Services**：在 Team Services 上创建生成定义时，只需在任意生成任务前将 [“NuGet 还原”](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) 或 [“.NET Core 还原”](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) 任务包括在定义中。</span><span class="sxs-lookup"><span data-stu-id="6deb1-131">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="6deb1-132">大量生成模板中默认包括了此任务。</span><span class="sxs-lookup"><span data-stu-id="6deb1-132">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="6deb1-133">**Team Foundation Server**：TFS 2013 和更高版本在生成期间会自动还原包，前提是使用适用于 TFS 2013 或更高版本的 Team Build Template。</span><span class="sxs-lookup"><span data-stu-id="6deb1-133">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="6deb1-134">对于更早版本的 TFS，可以包括一个生成步骤以调用上面其中一个命令行还原选项。</span><span class="sxs-lookup"><span data-stu-id="6deb1-134">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="6deb1-135">你可以选择将生成模板迁移到 TFS 2013。</span><span class="sxs-lookup"><span data-stu-id="6deb1-135">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="6deb1-136">有关详细信息，请参阅[使用 Team Foundation Build 还原包的演练](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-136">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="6deb1-137">启用和禁用包还原</span><span class="sxs-lookup"><span data-stu-id="6deb1-137">Enabling and disabling package restore</span></span>

<span data-ttu-id="6deb1-138">包还原主要通过 Visual Studio 中的“工具”>“选项”>“NuGet 包管理器”启用：</span><span class="sxs-lookup"><span data-stu-id="6deb1-138">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![通过NuGet 包管理器选项控制包还原行为](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="6deb1-140">**允许 NuGet 下载缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/enabled` 设置控制包还原的所有窗体（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-140">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="6deb1-141">在 Visual Studio 中，此设置可使解决方案上下文菜单中的 Restore NuGet Packages 命令正常工作。</span><span class="sxs-lookup"><span data-stu-id="6deb1-141">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="6deb1-142">可以通过在启动 Visual Studio 或启动生成前将名为 EnableNuGetPackageRestore 的环境变量设为 TRUE 或 FALSE 值，全局重写 `packageRestore/enabled` 设置。</span><span class="sxs-lookup"><span data-stu-id="6deb1-142">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="6deb1-143">**生成期间在 Visual Studio 中自动检查缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/automatic` 设置控制自动还原（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="6deb1-143">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="6deb1-144">设置此选项后，从 Visual Studio 运行生成会自动还原任何缺失的包。</span><span class="sxs-lookup"><span data-stu-id="6deb1-144">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="6deb1-145">该选项不影响使用 MSBuild 从命令行运行的生成。</span><span class="sxs-lookup"><span data-stu-id="6deb1-145">The option does not affect builds run from the command line using MSBuild.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="6deb1-146">有关引用，请参阅 [NuGet 配置文件 - packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-146">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="6deb1-147">在某些情况下，开发人员或公司可能希望对计算机上的所有用户启用或禁用包还原。</span><span class="sxs-lookup"><span data-stu-id="6deb1-147">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="6deb1-148">这可以通过将与以上相同的设置添加到位于 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 中的全局 NuGet 配置文件来完成。</span><span class="sxs-lookup"><span data-stu-id="6deb1-148">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="6deb1-149">然后，各个用户可以按照项目级别的要求有选择地启用还原。</span><span class="sxs-lookup"><span data-stu-id="6deb1-149">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="6deb1-150">有关 NuGet 如何设置多个配置文件优先级的确切详细信息，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-150">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="6deb1-151">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="6deb1-151">Constraining package versions with restore</span></span>

<span data-ttu-id="6deb1-152">NuGet 通过任意方法还原包时，它将遵守 `packages.config` 或项目文件中指定的任何约束：</span><span class="sxs-lookup"><span data-stu-id="6deb1-152">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="6deb1-153">`packages.config`：在依赖项的 `allowedVersion` 属性中指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="6deb1-153">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="6deb1-154">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-154">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="6deb1-155">例如:</span><span class="sxs-lookup"><span data-stu-id="6deb1-155">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="6deb1-156">PackageReference：使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="6deb1-156">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="6deb1-157">例如:</span><span class="sxs-lookup"><span data-stu-id="6deb1-157">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="6deb1-158">在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="6deb1-158">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6deb1-159">疑难解答</span><span class="sxs-lookup"><span data-stu-id="6deb1-159">Troubleshooting</span></span>

<span data-ttu-id="6deb1-160">请参阅[包还原疑难解答](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="6deb1-160">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>