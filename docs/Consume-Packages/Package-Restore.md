---
title: "NuGet 程序包还原 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "描述 NuGet 如何还原项目依赖的包，包括如何禁用还原和约束版本。"
keywords: "NuGet 包还原, NuGet 包安装, 安装包, 还原包, 依赖项版本, 禁用自动还原, 约束包版本"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="86185-104">包还原</span><span class="sxs-lookup"><span data-stu-id="86185-104">Package Restore</span></span>

<span data-ttu-id="86185-105">为了提升为更干净的开发环境并减少存储库大小，NuGet“包还原”在生成项目前会安装所有引用的包。</span><span class="sxs-lookup"><span data-stu-id="86185-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="86185-106">这种广泛使用的功能确保了所有依赖项在项目中均可用，无需那些包存储在源代码管理中（有关如何配置存储库排除包二进制文件的信息，请参阅[包与源代码管理](../consume-packages/packages-and-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="86185-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="86185-107">在本主题中：</span><span class="sxs-lookup"><span data-stu-id="86185-107">In this topic:</span></span>
- [<span data-ttu-id="86185-108">包还原快速指南</span><span class="sxs-lookup"><span data-stu-id="86185-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="86185-109">包还原概述</span><span class="sxs-lookup"><span data-stu-id="86185-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="86185-110">启用和禁用包还原</span><span class="sxs-lookup"><span data-stu-id="86185-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="86185-111">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="86185-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="86185-112">[命令行还原](#command-line-restore)，适用于 NuGet 的所有版本</span><span class="sxs-lookup"><span data-stu-id="86185-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="86185-113">[Visual Studio 中的自动还原](#automatic-restore-in-visual-studio)，适用于 NuGet 2.7 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="86185-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="86185-114">[Visual Studio 中集成 MSBuild 的存储](#msbuild-integrated-restore)，适用于 NuGet 2.6 和更早版本。</span><span class="sxs-lookup"><span data-stu-id="86185-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="86185-115">使用 Team Foundation Build 还原包</span><span class="sxs-lookup"><span data-stu-id="86185-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="86185-116">还原行为会随着版本变化，若要检查 NuGet 版本，只需在命令行上运行 `nuget.exe` 并查看输出的第一行。</span><span class="sxs-lookup"><span data-stu-id="86185-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="86185-117">有关生成服务器上的包还原的其他详细信息，请参阅[使用 TFBuild 还原包](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="86185-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="86185-118">为包还原配置的项目同样使用 Mono 上的 xbuild。</span><span class="sxs-lookup"><span data-stu-id="86185-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="86185-119">包还原快速指南</span><span class="sxs-lookup"><span data-stu-id="86185-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="86185-120">如果看到错误“此项目引用此计算机上缺少的 NuGet 包”或者“一个或更多 NuGet 包需要还原但无法还原，因为未授予许可”，则按照[启用和禁用包还原](#enabling-and-disabling-package-restore)中的以下说明打开自动还原。</span><span class="sxs-lookup"><span data-stu-id="86185-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="86185-121">包还原概述</span><span class="sxs-lookup"><span data-stu-id="86185-121">Package restore overview</span></span>

<span data-ttu-id="86185-122">首先，包引用按以下其中一种包管理格式保留，具体取决于项目类型和 NuGet 版本。</span><span class="sxs-lookup"><span data-stu-id="86185-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="86185-123">（注意 NuGet 4 和 MSBuild 15.1 是使用 Visual Studio 2017 安装的。）</span><span class="sxs-lookup"><span data-stu-id="86185-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="86185-124">方法</span><span class="sxs-lookup"><span data-stu-id="86185-124">Method</span></span> | <span data-ttu-id="86185-125">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="86185-125">NuGet Version</span></span> | <span data-ttu-id="86185-126">描述</span><span class="sxs-lookup"><span data-stu-id="86185-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="86185-127">2.x+</span><span class="sxs-lookup"><span data-stu-id="86185-127">2.x+</span></span> | <span data-ttu-id="86185-128">列出依赖项的完整深层集。</span><span class="sxs-lookup"><span data-stu-id="86185-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="86185-129">添加到 `packages.config` 的包还必须添加到项目文件，“目标”和“属性”也必须添加到项目文件。</span><span class="sxs-lookup"><span data-stu-id="86185-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="86185-130">这是适用于所有版本的 NuGet 的基线法，但是与其他选项相比性能较低。</span><span class="sxs-lookup"><span data-stu-id="86185-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="86185-131">（请参阅 [packages.config 架构](../schema/packages-config.md)。）</span><span class="sxs-lookup"><span data-stu-id="86185-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="86185-132">3.x+</span><span class="sxs-lookup"><span data-stu-id="86185-132">3.x+</span></span> | <span data-ttu-id="86185-133">默认情况下仅与 UWP 项目共同使用，但是可以从 `packages.config` 转换项目。</span><span class="sxs-lookup"><span data-stu-id="86185-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="86185-134">`project.json` 仅列出顶级依赖项。</span><span class="sxs-lookup"><span data-stu-id="86185-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="86185-135">生成期间，将“引用”、“目标”和“属性”动态添加到项目，获得比 `packages.config` 更好的性能。</span><span class="sxs-lookup"><span data-stu-id="86185-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="86185-136">（请参阅 [project.json 架构](../schema/project-json.md)。）</span><span class="sxs-lookup"><span data-stu-id="86185-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="86185-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="86185-137">PackageReference</span></span> | <span data-ttu-id="86185-138">4.x+</span><span class="sxs-lookup"><span data-stu-id="86185-138">4.x+</span></span> | <span data-ttu-id="86185-139">在 `<Reference>` 和 `<ProjectReference>` 旁的 `<PackageReference>` 节点的项目文件中直接列出依赖项。</span><span class="sxs-lookup"><span data-stu-id="86185-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="86185-140">工作原理类似 `project.json`请参阅[项目文件中的包引用](../Consume-Packages/Package-References-in-Project-Files.md)。</span><span class="sxs-lookup"><span data-stu-id="86185-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="86185-141">其次，使用引用列表通过多种方法开始还原：</span><span class="sxs-lookup"><span data-stu-id="86185-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="86185-142">从命令行或者[包管理器控制台](../tools/Package-Manager-Console.md)：</span><span class="sxs-lookup"><span data-stu-id="86185-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="86185-143">命令</span><span class="sxs-lookup"><span data-stu-id="86185-143">Command</span></span> | <span data-ttu-id="86185-144">适用方案</span><span class="sxs-lookup"><span data-stu-id="86185-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="86185-145">NuGet 所有版本和所有引用类型。</span><span class="sxs-lookup"><span data-stu-id="86185-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="86185-146">请参阅以下[命令行还原](#command-line-restore)。</span><span class="sxs-lookup"><span data-stu-id="86185-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="86185-147">与 .NET Core 项目的 `nuget restore` 相同。</span><span class="sxs-lookup"><span data-stu-id="86185-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="86185-148">请参阅 [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore)。</span><span class="sxs-lookup"><span data-stu-id="86185-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="86185-149">仅有[项目文件中的包引用](../Consume-Packages/Package-References-in-Project-Files.md)的 Nuget 4.x+ 和 MSBuild 15.1+。</span><span class="sxs-lookup"><span data-stu-id="86185-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="86185-150">`nuget restore` 和 `dotnet restore` 均对适用项目使用此命令。</span><span class="sxs-lookup"><span data-stu-id="86185-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="86185-151">请参阅[NuGet 打包和还原为 MSBuild 目标 - 还原目标](../schema/msbuild-targets.md#restore-target)。</span><span class="sxs-lookup"><span data-stu-id="86185-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="86185-152">Visual Studio 自身同样在不同时间还原包：</span><span class="sxs-lookup"><span data-stu-id="86185-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="86185-153">类型</span><span class="sxs-lookup"><span data-stu-id="86185-153">Type</span></span> | <span data-ttu-id="86185-154">还原发生时</span><span class="sxs-lookup"><span data-stu-id="86185-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="86185-155">模板还原</span><span class="sxs-lookup"><span data-stu-id="86185-155">Template restore</span></span> | <span data-ttu-id="86185-156">创建新项目期间，某些模板依赖外部包。</span><span class="sxs-lookup"><span data-stu-id="86185-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="86185-157">生成还原</span><span class="sxs-lookup"><span data-stu-id="86185-157">Build restore</span></span> | <span data-ttu-id="86185-158">作为生成第一步。</span><span class="sxs-lookup"><span data-stu-id="86185-158">As the first step of a build.</span></span> |
| <span data-ttu-id="86185-159">解决方案还原</span><span class="sxs-lookup"><span data-stu-id="86185-159">Solution restore</span></span> | <span data-ttu-id="86185-160">用户右键单击解决方案并选择“还原 NuGet 包”时。</span><span class="sxs-lookup"><span data-stu-id="86185-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="86185-161">项目更改上的还原</span><span class="sxs-lookup"><span data-stu-id="86185-161">Restore on project change</span></span> | <span data-ttu-id="86185-162">（仅 NuGet 4.x）使用基于 .NET Core SDK 的项目时，包括项目状态的更改时间。</span><span class="sxs-lookup"><span data-stu-id="86185-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="86185-163">启用和禁用包还原</span><span class="sxs-lookup"><span data-stu-id="86185-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="86185-164">包还原主要通过 Visual Studio 中的“工具”>“选项”>“NuGet 包管理器”启用：</span><span class="sxs-lookup"><span data-stu-id="86185-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![通过NuGet 包管理器选项控制包还原行为](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="86185-166">允许 NuGet 下载缺失的包：如下所示，通过更改 `%AppData%\NuGet\NuGet.Config` 文件中的 `packageRestore/enabled` 设置控制包还原的所有窗体。</span><span class="sxs-lookup"><span data-stu-id="86185-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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
    >  <span data-ttu-id="86185-167">可以通过在启动 Visual Studio 或启动生成前将名为 EnableNuGetPackageRestore 的环境变量设为 TRUE 或 FALSE 值，全局重写 `packageRestore/enabled` 设置。</span><span class="sxs-lookup"><span data-stu-id="86185-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="86185-168">**生成期间在 Visual Studio 中自动检查缺失的包**：如下所示，通过更改 `%AppData%\NuGet\NuGet.Config` 文件中的 `packageRestore/automatic` 设置，控制适用于 NuGet 2.7 和更改版本的自动还原。</span><span class="sxs-lookup"><span data-stu-id="86185-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
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

<span data-ttu-id="86185-169">有关引用，请参阅 [NuGet 配置文件 - packageRestore 部分](../Schema/nuget-config-file.md#packagerestore-section)。</span><span class="sxs-lookup"><span data-stu-id="86185-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="86185-170">在某些情况下，开发人员或公司可能希望默认情况下对所有用户在计算机上启用或禁用包还原。</span><span class="sxs-lookup"><span data-stu-id="86185-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="86185-171">这可以通过将与以上相同的设置添加到位于 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` 中的全局 NuGet 配置文件完成。</span><span class="sxs-lookup"><span data-stu-id="86185-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="86185-172">然后，各个用户可以按照项目级别的要求有选择地启用还原。</span><span class="sxs-lookup"><span data-stu-id="86185-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="86185-173">有关 NuGet 如何设置多个配置文件优先级的准确详细信息，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)。</span><span class="sxs-lookup"><span data-stu-id="86185-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="86185-174">使用还原约束包版本</span><span class="sxs-lookup"><span data-stu-id="86185-174">Constraining package versions with restore</span></span>

<span data-ttu-id="86185-175">NuGet 通过任意方法还原包时，它将遵守 `packages.config`、`project.json` 或项目文件中指定的任何约束：</span><span class="sxs-lookup"><span data-stu-id="86185-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="86185-176">`packages.config`：在依赖项的 `allowedVersion` 属性中指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="86185-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="86185-177">请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)。</span><span class="sxs-lookup"><span data-stu-id="86185-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="86185-178">例如: </span><span class="sxs-lookup"><span data-stu-id="86185-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="86185-179">`project.json` 使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="86185-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="86185-180">例如: </span><span class="sxs-lookup"><span data-stu-id="86185-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="86185-181">项目文件中的包引用：使用依赖项的版本号直接指定版本范围。</span><span class="sxs-lookup"><span data-stu-id="86185-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="86185-182">例如: </span><span class="sxs-lookup"><span data-stu-id="86185-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="86185-183">在所有情况下，都使用[包版本控制](../reference/package-versioning.md)中介绍的表示法。</span><span class="sxs-lookup"><span data-stu-id="86185-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="86185-184">命令行还原</span><span class="sxs-lookup"><span data-stu-id="86185-184">Command-line restore</span></span>

<span data-ttu-id="86185-185">对于 NuGet 2.7 和更高版本，使用 [Restore](../tools/cli-ref-restore.md) 命令还原解决方案的所有包（无论它使用 `packages.config`、`project.json` 还是项目文件中的包引用）。</span><span class="sxs-lookup"><span data-stu-id="86185-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="86185-186">对于 `c:\proj\app` 之类的给定项目文件夹，以下每个常见变体都会还原包：</span><span class="sxs-lookup"><span data-stu-id="86185-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="86185-187">对于 NuGet 4.0+ 和 MSBuild 15.1+，还可以使用 `MSBuild /t:restore`，如 [NuGet 打包和还原为 MSBuild 目标](../schema/msbuild-targets.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="86185-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="86185-188">Visual Studio 中的生成时还原</span><span class="sxs-lookup"><span data-stu-id="86185-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="86185-189">Visual Studio 默认在生成开始时自动还原缺失的包。</span><span class="sxs-lookup"><span data-stu-id="86185-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="86185-190">此行为可以通过清除“工具”>“选项”>“NuGet 包管理器”>“常规”>“生成期间在 Visual Studio 中自动检查缺失的包”进行更改。</span><span class="sxs-lookup"><span data-stu-id="86185-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="86185-191">启用时，自动还原的工作原理如下所示：</span><span class="sxs-lookup"><span data-stu-id="86185-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="86185-192">生成开始时，Visual Studio 指示 NuGet 还原包。</span><span class="sxs-lookup"><span data-stu-id="86185-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="86185-193">NuGet 以递归的方式在解决方案中查找所有 `packages.config` 文件、查找 `project.json` 文件或在项目文件中查找。</span><span class="sxs-lookup"><span data-stu-id="86185-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="86185-194">对于引用文件中列出的每个包，NuGet 都会检查它是否已存在于解决方案中（`packages` 文件夹、`project.lock.json` 或 `project.assets.json`，具体取决于项目是否使用 `packages.config`、`project.json` 或项目文件中的包引用）。</span><span class="sxs-lookup"><span data-stu-id="86185-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="86185-195">如果未找到包，则 NuGet 尝试先从缓存中检索包（请参阅[管理 NuGet 缓存](../consume-packages/managing-the-nuget-cache.md)。</span><span class="sxs-lookup"><span data-stu-id="86185-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="86185-196">如果在缓存中未找到包，则 NuGet 尝试从“工具”>“选项”>“NuGet 包管理器”>“包源”中列出的已启用源中，按照源出现的顺序下载包。</span><span class="sxs-lookup"><span data-stu-id="86185-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="86185-197">在这种情况下，NuGet 不指示查找包失败，除非检查完所有源，才报告列表中仅最后源出现失败。</span><span class="sxs-lookup"><span data-stu-id="86185-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="86185-198">此类错误还暗示着 包已不在其他任意源上，尽管那些源没有单独显示错误。</span><span class="sxs-lookup"><span data-stu-id="86185-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="86185-199">如果下载成功，则 NuGet 会缓存包并将其安装到解决方案（同样也会安装到 `packages` 文件夹 `project.lock.json` 或 `project.assets.json`）；否则，NuGet 和生成均失败。</span><span class="sxs-lookup"><span data-stu-id="86185-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="86185-200">在此过程中，会出现含有取消包还原选项的进度对话框。</span><span class="sxs-lookup"><span data-stu-id="86185-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="86185-201">使用 Team Foundation Build 还原包</span><span class="sxs-lookup"><span data-stu-id="86185-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="86185-202">在生成服务器上生成项目时通常会用到包还原，正如 Team Foundation Server (TFS) 和 Visual Studio Team Services（以及其他此处未涉及的生成系统）。</span><span class="sxs-lookup"><span data-stu-id="86185-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="86185-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="86185-203">Visual Studio Team Services</span></span>

<span data-ttu-id="86185-204">在 Team Services 上创建生成定义时，只需在任意生成任务前将“还原 NuGet 包”任务包括在定义中。</span><span class="sxs-lookup"><span data-stu-id="86185-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="86185-205">大量生成模板中默认包括了此任务。</span><span class="sxs-lookup"><span data-stu-id="86185-205">This task is included by default in a number of build templates.</span></span>

![Visual Studio Team Service 生成定义中的 NuGet 包还原任务](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="86185-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="86185-207">Team Foundation Server</span></span>

<span data-ttu-id="86185-208">使用 TFS 2013 和更高版本时，在生成期间会默认自动还原包，前提是使用适用于 Team Foundation Server 2013 或更高版本的 Team Build Template。</span><span class="sxs-lookup"><span data-stu-id="86185-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="86185-209">如果使用更早版本的生成模板（例如在从更早版本的 TFS 中迁移的项目中），则还需要将这些生成模板迁移到 TFS 2013。</span><span class="sxs-lookup"><span data-stu-id="86185-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="86185-210">这在本质上相当于使用适合源控件（TFVC 或 Git）的模板重新创建生成模板的自定义部分。</span><span class="sxs-lookup"><span data-stu-id="86185-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="86185-211">对于更早版本的 TFS，只需按照前面所述的方法，包括一个调用[命令行还原](#command-line-restore)的生成步骤。</span><span class="sxs-lookup"><span data-stu-id="86185-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="86185-212">有关详细信息，请参阅[使用 Team Foundation Build 还原包的演练](../consume-packages/team-foundation-build.md)。</span><span class="sxs-lookup"><span data-stu-id="86185-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
