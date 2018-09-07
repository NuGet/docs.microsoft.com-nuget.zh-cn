---
title: NuGet 包还原
description: 概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: b95c4462a214a78452f9dbe35936620636c4f60b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548767"
---
# <a name="package-restore"></a><span data-ttu-id="f30ae-103">包还原</span><span class="sxs-lookup"><span data-stu-id="f30ae-103">Package Restore</span></span>

<span data-ttu-id="f30ae-104">为了提升为更干净的开发环境并减少存储库大小，NuGet“包还原”安装项目在项目文件或 `packages.config` 中列出的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="f30ae-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all a project's dependencies as listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="f30ae-105">Visual Studio 可以在生成项目时自动还原包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-105">Visual Studio can restore packages automatically when a project is built.</span></span> <span data-ttu-id="f30ae-106">`dotnet build` 和 `dotnet run` 命令 (.NET Core 2.0+) 还执行自动还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-106">The `dotnet build` and `dotnet run` commands (.NET Core 2.0+) also perform an automatic restore.</span></span> <span data-ttu-id="f30ae-107">还可以随时通过 Visual Studio、`nuget restore`、`dotnet restore` 和 Mono 上的 xbuild 还原包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-107">You can also restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="f30ae-108">包还原确保项目的所有依赖项都可用，而无需在源代码管理中存储这些包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-108">Package restore makes sure that all a project's dependencies are available without storing those packages in source control.</span></span> <span data-ttu-id="f30ae-109">请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)，了解如何配置存储库以排除包二进制文件。</span><span class="sxs-lookup"><span data-stu-id="f30ae-109">See [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries.</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="f30ae-110">包还原概述</span><span class="sxs-lookup"><span data-stu-id="f30ae-110">Package restore overview</span></span>

<span data-ttu-id="f30ae-111">要还原包，首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="f30ae-111">Restoring packages first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="f30ae-112">如果尚未安装程序包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-global-packages-and-cache-folders.md)中检索它。</span><span class="sxs-lookup"><span data-stu-id="f30ae-112">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="f30ae-113">如果在缓存中未找到包，则 NuGet 将尝试从所有已启用的源下载该包（请参阅[配置 NuGet 行为](Configuring-NuGet-Behavior.md)）；源也会出现在 Visual Studio 的“工具”>“选项”>“NuGet 包管理器”>“包源”列表中。</span><span class="sxs-lookup"><span data-stu-id="f30ae-113">If the package is not in the cache, NuGet then attempts to download the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="f30ae-114">在还原期间，NuGet 会忽略包源的顺序，使用来自任何首先响应请求的源的包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-114">During restore, NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="f30ae-115">在检查完所有源之前，NuGet 不会指示包还原失败。</span><span class="sxs-lookup"><span data-stu-id="f30ae-115">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="f30ae-116">届时，NuGet 仅会报告列表中最后一个源的失败。</span><span class="sxs-lookup"><span data-stu-id="f30ae-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="f30ae-117">该错误说明包已不在其他任意源上，尽管那些源中的任何一个都没有单独显示错误。</span><span class="sxs-lookup"><span data-stu-id="f30ae-117">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="f30ae-118">包还原是通过以下方式触发的：</span><span class="sxs-lookup"><span data-stu-id="f30ae-118">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="f30ae-119">**dotnet CLI**：使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原项目文件中列出的包（请参阅 [PackageReference](../consume-packages/package-references-in-project-files.md)）。</span><span class="sxs-lookup"><span data-stu-id="f30ae-119">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="f30ae-120">使用 .NET Core 2.0 和更高版本，通过 `dotnet build` 和 `dotnet run` 自动完成还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-120">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="f30ae-121">**程序包管理器 UI（Windows 上的 Visual Studio）**：从模板创建项目以及构建项目时自动还原包（根据[启用和禁用包还原](#enabling-and-disabling-package-restore)中所述的选项）。</span><span class="sxs-lookup"><span data-stu-id="f30ae-121">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="f30ae-122">此外，在 NuGet 4.0+ 中，对基于 .NET Core SDK 的项目进行更改时还会自动进行还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-122">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="f30ae-123">要手动还原，请右键单击“解决方案资源管理器”中的解决方案，选择“还原 NuGet 包”。</span><span class="sxs-lookup"><span data-stu-id="f30ae-123">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="f30ae-124">如果一个或多个独立包仍未正确安装（即“解决方案资源管理器”显示错误图标），请使用程序包管理器 UI 卸载受影响的包并重新安装。</span><span class="sxs-lookup"><span data-stu-id="f30ae-124">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="f30ae-125">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f30ae-125">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="f30ae-126">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则按照[启用和禁用包还原](#enabling-and-disabling-package-restore)中的以下说明打开自动还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-126">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span> <span data-ttu-id="f30ae-127">另请参阅[包还原疑难解答](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-127">Also see [Package restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="f30ae-128">NuGet CLI：使用 [nuget restore](../tools/cli-ref-restore.md) 命令还原项目文件或 `packages.config` 中列出的包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-128">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file or in `packages.config`.</span></span> <span data-ttu-id="f30ae-129">此外，你还可以指定解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="f30ae-129">You can also specify a solution file.</span></span>

- <span data-ttu-id="f30ae-130">MSBuild：使用 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 命令还原项目文件中列出的包（仅限 PackageReference）。</span><span class="sxs-lookup"><span data-stu-id="f30ae-130">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (PackageReference only).</span></span> <span data-ttu-id="f30ae-131">仅适用于 Visual Studio 2017 附带的 NuGet 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="f30ae-131">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="f30ae-132">`nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。</span><span class="sxs-lookup"><span data-stu-id="f30ae-132">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="f30ae-133">**Visual Studio Team Services**：在 Team Services 上创建生成定义时，只需在任意生成任务前将 [“NuGet 还原”](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) 或 [“.NET Core 还原”](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) 任务包括在定义中。</span><span class="sxs-lookup"><span data-stu-id="f30ae-133">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="f30ae-134">大量生成模板中默认包括了此任务。</span><span class="sxs-lookup"><span data-stu-id="f30ae-134">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="f30ae-135">**Team Foundation Server**：TFS 2013 和更高版本在生成期间会自动还原包，前提是使用适用于 TFS 2013 或更高版本的 Team Build Template。</span><span class="sxs-lookup"><span data-stu-id="f30ae-135">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="f30ae-136">对于更早版本的 TFS，可以包括一个生成步骤以调用上面其中一个命令行还原选项。</span><span class="sxs-lookup"><span data-stu-id="f30ae-136">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="f30ae-137">你可以选择将生成模板迁移到 TFS 2013。</span><span class="sxs-lookup"><span data-stu-id="f30ae-137">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="f30ae-138">有关详细信息，请参阅[使用 Team Foundation Build 还原包的演练](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-138">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="f30ae-139">启用和禁用包还原</span><span class="sxs-lookup"><span data-stu-id="f30ae-139">Enabling and disabling package restore</span></span>

<span data-ttu-id="f30ae-140">包还原主要通过 Visual Studio 中的“工具”>“选项”>“NuGet 包管理器”启用：</span><span class="sxs-lookup"><span data-stu-id="f30ae-140">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![通过NuGet 包管理器选项控制包还原行为](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="f30ae-142">**允许 NuGet 下载缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/enabled` 设置控制包还原的所有窗体（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="f30ae-142">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="f30ae-143">在 Visual Studio 中，此设置可使解决方案上下文菜单中的 Restore NuGet Packages 命令正常工作。</span><span class="sxs-lookup"><span data-stu-id="f30ae-143">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

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
    >  <span data-ttu-id="f30ae-144">可以通过在启动 Visual Studio 或启动生成前将名为 EnableNuGetPackageRestore 的环境变量设为 TRUE 或 FALSE 值，全局重写 `packageRestore/enabled` 设置。</span><span class="sxs-lookup"><span data-stu-id="f30ae-144">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="f30ae-145">**生成期间在 Visual Studio 中自动检查缺失的包**：如下所示，通过更改 `NuGet.Config` 文件中的 `packageRestore/automatic` 设置控制自动还原（Windows 上为 `%AppData%\NuGet\NuGet.Config`，Mac/Linux 上为 `~/.nuget/NuGet/NuGet.Config`）。</span><span class="sxs-lookup"><span data-stu-id="f30ae-145">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="f30ae-146">设置此选项后，从 Visual Studio 运行生成会自动还原任何缺失的包。</span><span class="sxs-lookup"><span data-stu-id="f30ae-146">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="f30ae-147">该选项不影响使用 MSBuild 从命令行运行的生成。</span><span class="sxs-lookup"><span data-stu-id="f30ae-147">The option does not affect builds run from the command line using MSBuild.</span></span>

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

<span data-ttu-id="f30ae-148">有关引用，请参阅 [NuGet 配置文件 - packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-148">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="f30ae-149">在某些情况下，开发人员或公司可能希望对计算机上的所有用户启用或禁用包还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-149">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="f30ae-150">若要执行此操作，请将上面的相同设置添加到全局 NuGet 配置文件，该文件位于 `%ProgramData%\NuGet\Config`（Windows，可能在某个特定的 Visual Studio `\{IDE}\{Version}\{SKU}\` 文件夹下）或 `~/.local/share` (Mac/Linux)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-150">To do this, add the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config` (Windows, potentially under a specific `\{IDE}\{Version}\{SKU}\` folder for Visual Studio) or `~/.local/share` (Mac/Linux).</span></span> <span data-ttu-id="f30ae-151">然后，各个用户可以按照项目级别的要求有选择地启用还原。</span><span class="sxs-lookup"><span data-stu-id="f30ae-151">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="f30ae-152">有关 NuGet 如何设置多个配置文件优先级的确切详细信息，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-152">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

> [!Important]
> <span data-ttu-id="f30ae-153">如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值。</span><span class="sxs-lookup"><span data-stu-id="f30ae-153">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="f30ae-154">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="f30ae-154">Constraining package versions with restore</span></span>

<span data-ttu-id="f30ae-155">NuGet 通过任意方法还原包时，它将遵守 `packages.config` 或项目文件中指定的任何约束：</span><span class="sxs-lookup"><span data-stu-id="f30ae-155">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="f30ae-156">`packages.config`：在依赖项的 `allowedVersion` 属性中指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="f30ae-156">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="f30ae-157">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-157">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="f30ae-158">例如:</span><span class="sxs-lookup"><span data-stu-id="f30ae-158">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="f30ae-159">项目文件 (PackageReference)：使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="f30ae-159">Project file (PackageReference): Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="f30ae-160">例如:</span><span class="sxs-lookup"><span data-stu-id="f30ae-160">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="f30ae-161">在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="f30ae-161">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="forcing-restore-from-package-sources"></a><span data-ttu-id="f30ae-162">强制从包源还原</span><span class="sxs-lookup"><span data-stu-id="f30ae-162">Forcing restore from package sources</span></span>

<span data-ttu-id="f30ae-163">默认情况下，NuGet 还原操作使用 global-packages 和 http-cache 文件夹中的包，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="f30ae-163">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="f30ae-164">若要避免使用 global-packages 文件夹，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="f30ae-164">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="f30ae-165">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除文件夹</span><span class="sxs-lookup"><span data-stu-id="f30ae-165">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`</span></span>
- <span data-ttu-id="f30ae-166">在进行还原操作之前，使用下列方法之一暂时更改 global-packages 的位置：</span><span class="sxs-lookup"><span data-stu-id="f30ae-166">Temporarily change the location of the *global-packages* folder before the restore operation using one of the following methods:</span></span>
  - <span data-ttu-id="f30ae-167">将 NUGET_PACKAGES 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="f30ae-167">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="f30ae-168">创建 `NuGet.Config` 文件，将 `globalPackagesFolder`（如果使用 PackageReference）或 `repositoryPath`（如果使用 `packages.config`）设置为其他文件夹（请参阅[配置设置](../reference/nuget-config-file.md#config-section)）</span><span class="sxs-lookup"><span data-stu-id="f30ae-168">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder (see [configuration settings](../reference/nuget-config-file.md#config-section)</span></span>
  - <span data-ttu-id="f30ae-169">仅限 MSBuild：指定具有 `RestorePackagesPath` 属性的其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="f30ae-169">MSBuild only: specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="f30ae-170">若要避免将缓存用于 HTTP 源，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="f30ae-170">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="f30ae-171">将 `-NoCache` 选项与 `nuget restore` 结合使用，或者将 `--no-cache` 选项与 `dotnet restore` 结合使用。</span><span class="sxs-lookup"><span data-stu-id="f30ae-171">Use the `-NoCache` option with `nuget restore` or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="f30ae-172">这些选项不会影响通过 Visual Studio 包管理器 UI 或控制台执行的还原操作。</span><span class="sxs-lookup"><span data-stu-id="f30ae-172">These options do not affect restore operations through the Visual Studio Package Manager UI or Console.</span></span>
- <span data-ttu-id="f30ae-173">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear` 清除缓存。</span><span class="sxs-lookup"><span data-stu-id="f30ae-173">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="f30ae-174">暂时将 NUGET_HTTP_CACHE_PATH 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="f30ae-174">Temporarily set of the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f30ae-175">疑难解答</span><span class="sxs-lookup"><span data-stu-id="f30ae-175">Troubleshooting</span></span>

<span data-ttu-id="f30ae-176">请参阅[包还原疑难解答](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="f30ae-176">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>