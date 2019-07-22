---
title: NuGet 包还原
description: 概述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: e85d8cc3fd9492118bd8f34cfd05f20a9724c281
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842343"
---
# <a name="package-restore-options"></a><span data-ttu-id="15d22-103">包还原选项</span><span class="sxs-lookup"><span data-stu-id="15d22-103">Package Restore options</span></span>

<span data-ttu-id="15d22-104">为了促成更干净的开发环境并减少存储库大小，NuGet“包还原”安装在项目文件或 `packages.config` 中列出的所有项目依赖项  。</span><span class="sxs-lookup"><span data-stu-id="15d22-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="15d22-105">.NET Core 2.0+ `dotnet build` 和 `dotnet run` 命令执行自动包还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="15d22-106">Visual Studio 可以在构建项目时自动还原包，并且你可以随时通过 Visual Studio、`nuget restore`、`dotnet restore` 和 xoild 在 Mono 上还原包。</span><span class="sxs-lookup"><span data-stu-id="15d22-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="15d22-107">包还原确保所有项目的依赖项都可用，无需将其存储在源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="15d22-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="15d22-108">要配置源代码管理存储库以排除包二进制文件，请参阅[包和源代码管理](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="15d22-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="15d22-109">包还原概述</span><span class="sxs-lookup"><span data-stu-id="15d22-109">Package Restore overview</span></span>

<span data-ttu-id="15d22-110">包还原首先根据需要安装项目的直接依赖项，然后在整个依赖项关系图中安装这些包的所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="15d22-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="15d22-111">如果尚未安装包，NuGet 首先尝试从[缓存](../consume-packages/managing-the-global-packages-and-cache-folders.md)中检索它。</span><span class="sxs-lookup"><span data-stu-id="15d22-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="15d22-112">如果包不在缓存中，NuGet 将尝试从 Visual Studio 的“工具” > “选项” > “NuGet 包管理器” > “包源”下的列表中的所有已启用的源下载包     。</span><span class="sxs-lookup"><span data-stu-id="15d22-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="15d22-113">在还原期间，NuGet 会忽略包源的顺序，使用来自任何首先响应请求的源的包。</span><span class="sxs-lookup"><span data-stu-id="15d22-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="15d22-114">有关 NuGet 的行为方式的详细信息，请参阅[常见的 NuGet 配置](Configuring-NuGet-Behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="15d22-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="15d22-115">在检查完所有源之前，NuGet 不会指示包还原失败。</span><span class="sxs-lookup"><span data-stu-id="15d22-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="15d22-116">届时，NuGet 仅会报告列表中最后一个源的失败。</span><span class="sxs-lookup"><span data-stu-id="15d22-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="15d22-117">该错误说明包已不在其他任意源上，尽管那些源中的任何一个都没有单独显示错误  。</span><span class="sxs-lookup"><span data-stu-id="15d22-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="15d22-118">还原包</span><span class="sxs-lookup"><span data-stu-id="15d22-118">Restore packages</span></span>

<span data-ttu-id="15d22-119">可以通过以下任一方式触发包还原：</span><span class="sxs-lookup"><span data-stu-id="15d22-119">You can trigger Package Restore in any of the following ways:</span></span>

- <span data-ttu-id="15d22-120">**Visual Studio**：在 Windows 上的 Visual Studio 中，使用以下方法之一。</span><span class="sxs-lookup"><span data-stu-id="15d22-120">**Visual Studio**: In Visual Studio on Windows, use one of the following methods.</span></span>

    - <span data-ttu-id="15d22-121">自动还原包。</span><span class="sxs-lookup"><span data-stu-id="15d22-121">Restore packages automatically.</span></span> <span data-ttu-id="15d22-122">当根据[启用和禁用包还原](#enable-and-disable-package-restore-visual-studio)中的选项，从模板创建项目或生成项目时会自动执行包还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-122">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="15d22-123">此外，在 NuGet 4.0+ 中，对 SDK 样式的项目（通常是 .NET Core 或 .NET Standard 项目）进行更改时还会自动进行还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-123">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

    - <span data-ttu-id="15d22-124">手动还原包。</span><span class="sxs-lookup"><span data-stu-id="15d22-124">Restore packages manually.</span></span> <span data-ttu-id="15d22-125">要手动还原，请右键单击解决方案资源管理器中的解决方案，选择“还原 NuGet 包”   。</span><span class="sxs-lookup"><span data-stu-id="15d22-125">To restore manually, right-click the solution in **Solution Explorer** and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="15d22-126">如果仍未正确安装一个或多个单独的包，“解决方案资源管理器”会显示错误图标  。</span><span class="sxs-lookup"><span data-stu-id="15d22-126">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="15d22-127">右键单击并选择“管理 NuGet 包”，然后使用“包管理器”卸载并重新安装受影响的包   。</span><span class="sxs-lookup"><span data-stu-id="15d22-127">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="15d22-128">有关详细信息，请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)</span><span class="sxs-lookup"><span data-stu-id="15d22-128">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="15d22-129">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则[启用自动还原](#enable-and-disable-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="15d22-129">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="15d22-130">此外，请参阅[迁移到自动包还原](#migrate-to-automatic-package-restore-visual-studio)和[包还原故障排除](Package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="15d22-130">Also, see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio) and [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="15d22-131">**dotnet CLI**：在命令行中，切换到包含项目的文件夹，然后使用 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 命令还原带有 [PackageReference](../consume-packages/package-references-in-project-files.md) 的项目文件中列出的包。</span><span class="sxs-lookup"><span data-stu-id="15d22-131">**dotnet CLI**: In the command line, switch to the folder that contains your project, and then use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command to restore packages listed in the project file with [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span> <span data-ttu-id="15d22-132">如果为 .NET Core 2.0 和更高版本，使用 `dotnet build` 和 `dotnet run` 命令可以自动进行还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-132">With .NET Core 2.0 and later, restore happens automatically with the `dotnet build` and `dotnet run` commands.</span></span>  

- <span data-ttu-id="15d22-133">**nuget.exe CLI**：在命令行中，切换到包含项目的文件夹，然后使用 [nuget restore](../tools/cli-ref-restore.md) 命令还原项目或解决方案文件或 `packages.config` 中列出的包。</span><span class="sxs-lookup"><span data-stu-id="15d22-133">**nuget.exe CLI**: In the command line, switch to the folder that contains your project, and then use the [nuget restore](../tools/cli-ref-restore.md) command to restore packages listed in a project or solution file, or in `packages.config`.</span></span> 

- <span data-ttu-id="15d22-134">**MSBuild**：使用 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 命令通过 PackageReference 还原项目文件中列出的包。</span><span class="sxs-lookup"><span data-stu-id="15d22-134">**MSBuild**: Use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command to restore packages listed in the project file with PackageReference.</span></span> <span data-ttu-id="15d22-135">此命令仅适用于 Visual Studio 2017 及更高版本附带的 NuGet 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="15d22-135">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="15d22-136">`nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。</span><span class="sxs-lookup"><span data-stu-id="15d22-136">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

- <span data-ttu-id="15d22-137">**Azure Pipelines**：在 Azure Pipelines 上创建生成定义时，请在任意生成任务前将 NuGet [还原](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 或 .NET Core [还原](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 任务包括在定义中。</span><span class="sxs-lookup"><span data-stu-id="15d22-137">**Azure Pipelines**: When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="15d22-138">默认情况下，某些生成模板包括还原任务。</span><span class="sxs-lookup"><span data-stu-id="15d22-138">Some build templates include the restore task by default.</span></span>

- <span data-ttu-id="15d22-139">**Azure DevOps Server**：如果你使用的是 TFS 2013 或更高版本的 Team Build 模板，Azure DevOps Server 和 TFS 2013 及更高版本会在生成期间自动还原包。</span><span class="sxs-lookup"><span data-stu-id="15d22-139">**Azure DevOps Server**: Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="15d22-140">对于较早的 TFS 版本，可以包含一个生成步骤来运行命令行还原选项，或者选择将生成模板迁移到更高版本。</span><span class="sxs-lookup"><span data-stu-id="15d22-140">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="15d22-141">有关详细信息，请参阅[使用 Team Foundation Build 设置包还原](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="15d22-141">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enable-and-disable-package-restore-visual-studio"></a><span data-ttu-id="15d22-142">启用和禁用包还原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="15d22-142">Enable and disable package restore (Visual Studio)</span></span>

<span data-ttu-id="15d22-143">在 Visual Studio 中，主要通过“工具” > “选项” > “NuGet 包管理器”控制包还原    ：</span><span class="sxs-lookup"><span data-stu-id="15d22-143">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![通过 NuGet 包管理器选项控制包还原](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="15d22-145">“允许 NuGet 下载缺失的包”通过更改 `NuGet.Config` 文件中的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)的 `packageRestore/enabled` 设置控制包还原的所有窗体（该文件在 Windows 上位于 `%AppData%\NuGet\`，在 Mac/Linux 上位于 `~/.nuget/NuGet/`）  。</span><span class="sxs-lookup"><span data-stu-id="15d22-145">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="15d22-146">在 Visual Studio 中，此设置还可启用解决方案上下文菜单中的 Restore NuGet Packages 命令  。</span><span class="sxs-lookup"><span data-stu-id="15d22-146">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > <span data-ttu-id="15d22-147">要全局重写 `packageRestore/enabled` 设置，请在启动 Visual Studio 或启动生成之前，将 EnableNuGetPackageRestore 环境变量设为 TRUE 或 FALSE 值  。</span><span class="sxs-lookup"><span data-stu-id="15d22-147">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="15d22-148">“生成期间在 Visual Studio 中自动检查缺失的包”通过更改 `NuGet.Config` 文件的 [packageRestore 部分](../reference/nuget-config-file.md#packagerestore-section)中的 `packageRestore/automatic` 设置控制自动还原  。</span><span class="sxs-lookup"><span data-stu-id="15d22-148">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="15d22-149">将该选项设置为 True 后，从 Visual Studio 运行生成会自动还原任何缺失的包。</span><span class="sxs-lookup"><span data-stu-id="15d22-149">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="15d22-150">此设置不会影响从 MSBuild 命令行运行的生成。</span><span class="sxs-lookup"><span data-stu-id="15d22-150">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="15d22-151">要为计算机上的所有用户启用或禁用包还原，开发人员或公司可以将配置设置添加到全局 `nuget.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="15d22-151">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="15d22-152">全局 `nuget.config` 在 Windows 中位于 `%ProgramData%\NuGet\Config` 下，有时在特定的 `\{IDE}\{Version}\{SKU}\`Visual Studio 文件夹下，或者在 Mac/Linux 中位于 `~/.local/share` 下。</span><span class="sxs-lookup"><span data-stu-id="15d22-152">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="15d22-153">然后，各个用户可以按照项目级别的要求有选择地启用还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-153">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="15d22-154">有关 NuGet 如何设置多个配置文件优先级的详细信息，请参阅[常见 NuGet 配置](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="15d22-154">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="15d22-155">如果直接在 `nuget.config` 中编辑 `packageRestore` 设置，请重启 Visual Studio，以便“选项”对话框显示当前值  。</span><span class="sxs-lookup"><span data-stu-id="15d22-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="15d22-156">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="15d22-156">Constrain package versions with restore</span></span>

<span data-ttu-id="15d22-157">NuGet 通过任意方法还原包时，将遵守你在 `packages.config` 或项目文件中指定的任何约束：</span><span class="sxs-lookup"><span data-stu-id="15d22-157">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="15d22-158">在 `packages.config` 中，可在依赖项的 `allowedVersion` 属性中指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="15d22-158">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="15d22-159">有关详细信息，请参阅[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="15d22-159">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="15d22-160">例如:</span><span class="sxs-lookup"><span data-stu-id="15d22-160">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="15d22-161">在项目文件中，可以使用 PackageReference 直接指定依赖项的范围。</span><span class="sxs-lookup"><span data-stu-id="15d22-161">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="15d22-162">例如:</span><span class="sxs-lookup"><span data-stu-id="15d22-162">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="15d22-163">在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="15d22-163">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="15d22-164">强制从包源还原</span><span class="sxs-lookup"><span data-stu-id="15d22-164">Force restore from package sources</span></span>

<span data-ttu-id="15d22-165">默认情况下，NuGet 还原操作使用 global-packages 和 http-cache 文件夹中的包，如[管理全局包和缓存文件夹](managing-the-global-packages-and-cache-folders.md)中所述   。</span><span class="sxs-lookup"><span data-stu-id="15d22-165">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="15d22-166">若要避免使用 global-packages  文件夹，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="15d22-166">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="15d22-167">使用 `nuget locals global-packages -clear` 或 `dotnet nuget locals global-packages --clear` 清除文件夹。</span><span class="sxs-lookup"><span data-stu-id="15d22-167">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="15d22-168">在进行还原操作之前，使用下列方法之一暂时更改 global-packages 的位置  ：</span><span class="sxs-lookup"><span data-stu-id="15d22-168">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="15d22-169">将 NUGET_PACKAGES 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="15d22-169">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="15d22-170">创建 `NuGet.Config` 文件，将 `globalPackagesFolder`（如果使用 PackageReference）或 `repositoryPath`（如果使用 `packages.config`）设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="15d22-170">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="15d22-171">有关详细信息，请参阅[配置设置](../reference/nuget-config-file.md#config-section)。</span><span class="sxs-lookup"><span data-stu-id="15d22-171">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="15d22-172">仅限 MSBuild：指定具有 `RestorePackagesPath` 属性的其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="15d22-172">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="15d22-173">若要避免将缓存用于 HTTP 源，请执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="15d22-173">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="15d22-174">将 `-NoCache` 选项与 `nuget restore` 结合使用，或者将 `--no-cache` 选项与 `dotnet restore` 结合使用。</span><span class="sxs-lookup"><span data-stu-id="15d22-174">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="15d22-175">这些选项不会影响通过 Visual Studio 包管理器或控制台执行的还原操作。</span><span class="sxs-lookup"><span data-stu-id="15d22-175">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="15d22-176">使用 `nuget locals http-cache -clear` 或 `dotnet nuget locals http-cache --clear` 清除缓存。</span><span class="sxs-lookup"><span data-stu-id="15d22-176">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="15d22-177">暂时将 NUGET_HTTP_CACHE_PATH 环境变量设置为其他文件夹。</span><span class="sxs-lookup"><span data-stu-id="15d22-177">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="15d22-178">迁移到自动包还原 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="15d22-178">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="15d22-179">对于 NuGet 2.6 及更早版本，以前支持集成 MSBuild 的包恢复，但现在不再支持。</span><span class="sxs-lookup"><span data-stu-id="15d22-179">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="15d22-180">（通常通过右键单击 Visual Studio 中的解决方案并选择“启用 NuGet 包还原”  来启用）。</span><span class="sxs-lookup"><span data-stu-id="15d22-180">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="15d22-181">如果项目使用已弃用的集成 MSBuild 的包还原，请迁移到自动包还原。</span><span class="sxs-lookup"><span data-stu-id="15d22-181">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="15d22-182">使用集成 MSBuild 的包还原的项目通常包含带有三个文件的 .nuget  文件夹：NuGet.config  、nuget.exe  和 NuGet.targets  。</span><span class="sxs-lookup"><span data-stu-id="15d22-182">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="15d22-183">若存在 NuGet.targets  文件，将确定 NuGet 是否将继续使用集成 MSBuild 的方法，因此在迁移期间必须删除此文件。</span><span class="sxs-lookup"><span data-stu-id="15d22-183">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="15d22-184">要迁移到自动包还原，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="15d22-184">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="15d22-185">关闭 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="15d22-185">Close Visual Studio.</span></span>
2. <span data-ttu-id="15d22-186">删除 .nuget/nuget.exe  和 .nuget/NuGet.targets  。</span><span class="sxs-lookup"><span data-stu-id="15d22-186">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="15d22-187">对于每个项目文件，删除 `<RestorePackages>` 元素并删除对 NuGet.targets  的任何引用。</span><span class="sxs-lookup"><span data-stu-id="15d22-187">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="15d22-188">要测试自动包还原，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="15d22-188">To test the automatic package restore:</span></span>

1. <span data-ttu-id="15d22-189">删除解决方案中的“packages”文件夹  。</span><span class="sxs-lookup"><span data-stu-id="15d22-189">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="15d22-190">在 Visual Studio 中打开解决方案并开始生成。</span><span class="sxs-lookup"><span data-stu-id="15d22-190">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="15d22-191">自动包还原应下载并安装每个依赖包，而不将它们添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="15d22-191">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="15d22-192">疑难解答</span><span class="sxs-lookup"><span data-stu-id="15d22-192">Troubleshooting</span></span>

<span data-ttu-id="15d22-193">请参阅[包还原疑难解答](package-restore-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="15d22-193">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
