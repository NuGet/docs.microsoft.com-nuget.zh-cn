---
title: 从 package.config 迁移到 PackageReference 格式
description: 详细介绍了如何将项目从 packages.config 管理格式迁移到 NuGet 4.0+、VS2017 以及 .NET Core 2.0 支持的 PackageReference
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 23bd936707173f49a651a8ba432fa8773fa53881
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237830"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="3af55-103">从 packages.config 迁移到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="3af55-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="3af55-104">Visual Studio 2017 版本 15.7 及更高版本支持将项目从 [packages.config](../reference/packages-config.md) 管理格式迁移到 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。</span><span class="sxs-lookup"><span data-stu-id="3af55-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="3af55-105">使用 PackageReference 的好处</span><span class="sxs-lookup"><span data-stu-id="3af55-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="3af55-106">**在一个位置管理所有项目依赖项** ：与项目到项目的引用和程序集引用一样，NuGet 包引用（使用 `PackageReference` 节点）直接在项目文件中进行管理，而不是使用单独的 packages.config 文件进行管理。</span><span class="sxs-lookup"><span data-stu-id="3af55-106">**Manage all project dependencies in one place** : Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="3af55-107">**顶级依赖项的有序视图** ：与 packages.config 不同，PackageReference 仅列出那些直接安装在项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="3af55-107">**Uncluttered view of top-level dependencies** : Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="3af55-108">因此，NuGet 包管理器 UI 和项目文件不会与低级依赖项混在一起。</span><span class="sxs-lookup"><span data-stu-id="3af55-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="3af55-109">**性能改进** ：使用 PackageReference 时，包保留在 global-packages  文件夹中（而不是解决方案中的 `packages` 文件夹中），如 [管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="3af55-109">**Performance improvements** : When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="3af55-110">因此，PackageReference 的执行速度更快，但占用的磁盘空间更少。</span><span class="sxs-lookup"><span data-stu-id="3af55-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="3af55-111">**更好地控制依赖项和内容流** ：使用 MSBuild 的现有功能可以 [有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)，并选择每个目标框架、配置、平台或其他透视的包引用。</span><span class="sxs-lookup"><span data-stu-id="3af55-111">**Fine control over dependencies and content flow** : Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="3af55-112">**PackageReference 正处于积极开发阶段** ：请参阅 [GitHub 上的 PackageReference 问题](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="3af55-112">**PackageReference is under active development** : See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="3af55-113">packages.config 不再处于积极开发阶段。</span><span class="sxs-lookup"><span data-stu-id="3af55-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="3af55-114">限制</span><span class="sxs-lookup"><span data-stu-id="3af55-114">Limitations</span></span>

* <span data-ttu-id="3af55-115">NuGet PackageReference 在 Visual Studio 2015 及更早版本中不可用。</span><span class="sxs-lookup"><span data-stu-id="3af55-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="3af55-116">只能在 Visual Studio 2017 及更高版本中打开已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="3af55-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="3af55-117">目前，C++ 和 ASP.NET 项目无法进行迁移。</span><span class="sxs-lookup"><span data-stu-id="3af55-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="3af55-118">某些包可能与 PackageReference 不完全兼容。</span><span class="sxs-lookup"><span data-stu-id="3af55-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="3af55-119">有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="3af55-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

<span data-ttu-id="3af55-120">此外，PackageReferences 的工作原理与 packages.config 相比存在一些差异。例如，PackageReference 不支持[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)，但添加了对[可变版本](../consume-packages/package-references-in-project-files.md#floating-versions)的支持。</span><span class="sxs-lookup"><span data-stu-id="3af55-120">In addition, there are some differences in how PackageReferences work compared to packages.config. For example - [constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) is not supprted by PackageReference but add support for [Floating Versions](../consume-packages/package-references-in-project-files.md#floating-versions).</span></span>

### <a name="known-issues"></a><span data-ttu-id="3af55-121">已知问题</span><span class="sxs-lookup"><span data-stu-id="3af55-121">Known Issues</span></span>

1. <span data-ttu-id="3af55-122">`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用</span><span class="sxs-lookup"><span data-stu-id="3af55-122">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="3af55-123">问题</span><span class="sxs-lookup"><span data-stu-id="3af55-123">Issue</span></span> 
 
<span data-ttu-id="3af55-124">首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。</span><span class="sxs-lookup"><span data-stu-id="3af55-124">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="3af55-125">这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="3af55-125">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="3af55-126">解决方法</span><span class="sxs-lookup"><span data-stu-id="3af55-126">Workaround</span></span> 

<span data-ttu-id="3af55-127">执行以下 NuGet 操作之一：</span><span class="sxs-lookup"><span data-stu-id="3af55-127">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="3af55-128">打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="3af55-128">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="3af55-129">打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="3af55-129">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="3af55-130">运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="3af55-130">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="3af55-131">生成还会触发 NuGet 还原的项目</span><span class="sxs-lookup"><span data-stu-id="3af55-131">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="3af55-132">现在应能够看到迁移选项。</span><span class="sxs-lookup"><span data-stu-id="3af55-132">You should now be able to see the migration option.</span></span> <span data-ttu-id="3af55-133">请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。</span><span class="sxs-lookup"><span data-stu-id="3af55-133">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="3af55-134">迁移步骤</span><span class="sxs-lookup"><span data-stu-id="3af55-134">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="3af55-135">在开始迁移之前，Visual Studio 会创建项目的备份，以便在必要时[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)。</span><span class="sxs-lookup"><span data-stu-id="3af55-135">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="3af55-136">使用 `packages.config` 打开包含项目的解决方案。</span><span class="sxs-lookup"><span data-stu-id="3af55-136">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="3af55-137">在“解决方案资源管理器”中，右键单击“引用”节点或 `packages.config` 文件，然后选择“将 packages.config 迁移到 PackageReference...”    。</span><span class="sxs-lookup"><span data-stu-id="3af55-137">In **Solution Explorer** , right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="3af55-138">迁移程序将分析项目的 NuGet 包引用并尝试将它们分类为“顶级依赖项”  （直接安装的 NuGet 包）和  “可传递的依赖项”（作为顶级包的依赖项安装的包）。</span><span class="sxs-lookup"><span data-stu-id="3af55-138">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="3af55-139">PackageReference 支持可传递包还原并动态解析依赖项，这意味着无需显式安装可传递的依赖项。</span><span class="sxs-lookup"><span data-stu-id="3af55-139">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="3af55-140">（可选）可以选择将分类为可传递的依赖项的 NuGet 包视为顶级依赖项，方法是为包选择  “顶级”选项。</span><span class="sxs-lookup"><span data-stu-id="3af55-140">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="3af55-141">对于包含不以可传递的方式流式传输的资产（`build`、`buildCrossTargeting`、`contentFiles` 或 `analyzers` 文件夹中的资产）以及标记为开发依赖项 (`developmentDependency = "true"`) 的资产的包，将自动设置此选项。</span><span class="sxs-lookup"><span data-stu-id="3af55-141">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="3af55-142">查看任何[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="3af55-142">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="3af55-143">选择“确定”  ，开始迁移。</span><span class="sxs-lookup"><span data-stu-id="3af55-143">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="3af55-144">迁移结束时，Visual Studio 会提供一个报表，其中包含指向备份的路径、已安装包的列表（顶级依赖项）、作为可传递的依赖项引用的包的列表以及在开始迁移时确定的兼容性问题的列表。</span><span class="sxs-lookup"><span data-stu-id="3af55-144">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="3af55-145">该报表将保存到备份文件夹。</span><span class="sxs-lookup"><span data-stu-id="3af55-145">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="3af55-146">验证解决方案是否生成并运行。</span><span class="sxs-lookup"><span data-stu-id="3af55-146">Validate that the solution builds and runs.</span></span> <span data-ttu-id="3af55-147">如果遇到问题，请[在 GitHub 上提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="3af55-147">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="3af55-148">如何回滚到 packages.config</span><span class="sxs-lookup"><span data-stu-id="3af55-148">How to roll back to packages.config</span></span>

1. <span data-ttu-id="3af55-149">关闭已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="3af55-149">Close the migrated project.</span></span>

1. <span data-ttu-id="3af55-150">将项目文件和 `packages.config` 从备份（通常为 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`）复制到项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="3af55-150">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="3af55-151">如果项目根目录中存在 obj 文件夹，则删除该文件夹。</span><span class="sxs-lookup"><span data-stu-id="3af55-151">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="3af55-152">打开项目。</span><span class="sxs-lookup"><span data-stu-id="3af55-152">Open the project.</span></span>

1. <span data-ttu-id="3af55-153">使用“工具”>“NuGet 包管理器”>“包管理器控制台”菜单命令打开包管理器控制台  。</span><span class="sxs-lookup"><span data-stu-id="3af55-153">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="3af55-154">在控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3af55-154">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="3af55-155">迁移后创建包</span><span class="sxs-lookup"><span data-stu-id="3af55-155">Create a package after migration</span></span>

<span data-ttu-id="3af55-156">迁移完成后，建议你添加对 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 包的引用，然后使用 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) 来创建包。</span><span class="sxs-lookup"><span data-stu-id="3af55-156">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="3af55-157">尽管在某些情况下可以使用 `dotnet.exe pack` 而不是 `msbuild -t:pack`，但不建议使用。</span><span class="sxs-lookup"><span data-stu-id="3af55-157">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="3af55-158">包兼容性问题</span><span class="sxs-lookup"><span data-stu-id="3af55-158">Package compatibility issues</span></span>

<span data-ttu-id="3af55-159">PackageReference 不支持 packages.config 支持的某些方面。</span><span class="sxs-lookup"><span data-stu-id="3af55-159">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="3af55-160">迁移程序将分析并检测此类问题。</span><span class="sxs-lookup"><span data-stu-id="3af55-160">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="3af55-161">具有以下一个或多个问题的任何包在迁移后可能无法按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="3af55-161">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="3af55-162">如果在迁移后安装了包，则将忽略“install.ps1”脚本</span><span class="sxs-lookup"><span data-stu-id="3af55-162">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3af55-163">**说明**</span><span class="sxs-lookup"><span data-stu-id="3af55-163">**Description**</span></span> | <span data-ttu-id="3af55-164">借助 PackageReference，安装或卸载包时不会执行 install.ps1 和 uninstall.ps1 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="3af55-164">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="3af55-165">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="3af55-165">**Potential impact**</span></span> | <span data-ttu-id="3af55-166">依赖于这些脚本来配置目标项目中的某些行为的包可能无法按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="3af55-166">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="3af55-167">如果在迁移后安装了包，则“内容”资产不可用</span><span class="sxs-lookup"><span data-stu-id="3af55-167">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3af55-168">**说明**</span><span class="sxs-lookup"><span data-stu-id="3af55-168">**Description**</span></span> | <span data-ttu-id="3af55-169">包的 `content` 文件夹中的资产不受 PackageReference 支持，并且将被忽略。</span><span class="sxs-lookup"><span data-stu-id="3af55-169">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="3af55-170">PackageReference 添加了对 `contentFiles` 的支持，以便获得更好的可传递支持和共享内容。</span><span class="sxs-lookup"><span data-stu-id="3af55-170">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="3af55-171">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="3af55-171">**Potential impact**</span></span> | <span data-ttu-id="3af55-172">`content` 中的资产不会复制到项目中，依赖于这些资产的项目代码需要重构。</span><span class="sxs-lookup"><span data-stu-id="3af55-172">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="3af55-173">如果在升级后安装了包，则不会应用 XDT 转换</span><span class="sxs-lookup"><span data-stu-id="3af55-173">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3af55-174">**说明**</span><span class="sxs-lookup"><span data-stu-id="3af55-174">**Description**</span></span> | <span data-ttu-id="3af55-175">PackageReference 不支持 XDT 转换，因此在安装或卸载包时将忽略 `.xdt` 文件。</span><span class="sxs-lookup"><span data-stu-id="3af55-175">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="3af55-176">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="3af55-176">**Potential impact**</span></span> | <span data-ttu-id="3af55-177">XDT 转换不会应用于任何项目 XML 文件（最常见的是 `web.config.install.xdt` 和 `web.config.uninstall.xdt`），这意味着在安装或卸载包时不会更新项目的 ` web.config` 文件。</span><span class="sxs-lookup"><span data-stu-id="3af55-177">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="3af55-178">如果在迁移后安装了包，则将忽略 lib 根目录中的程序集</span><span class="sxs-lookup"><span data-stu-id="3af55-178">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="3af55-179">**说明**</span><span class="sxs-lookup"><span data-stu-id="3af55-179">**Description**</span></span> | <span data-ttu-id="3af55-180">借助 PackageReference，将忽略无目标框架特定子文件夹的 `lib` 文件夹的根目录中的程序集。</span><span class="sxs-lookup"><span data-stu-id="3af55-180">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="3af55-181">NuGet 会查找与对应于项目的目标框架的目标框架名字对象 (TFM) 相匹配的子文件夹，并将匹配的程序集安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="3af55-181">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="3af55-182">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="3af55-182">**Potential impact**</span></span> | <span data-ttu-id="3af55-183">没有与对应于项目的目标框架的目标框架名字对象 (TFM) 相匹配的子文件夹的包在迁移期间转换或安装失败后可能无法按预期方式工作</span><span class="sxs-lookup"><span data-stu-id="3af55-183">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="3af55-184">如果发现错误，</span><span class="sxs-lookup"><span data-stu-id="3af55-184">Found an issue?</span></span> <span data-ttu-id="3af55-185">请将其报告！</span><span class="sxs-lookup"><span data-stu-id="3af55-185">Report it!</span></span>

<span data-ttu-id="3af55-186">如果在迁移过程中遇到问题，请[在 NuGet GitHub 存储库上提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="3af55-186">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
