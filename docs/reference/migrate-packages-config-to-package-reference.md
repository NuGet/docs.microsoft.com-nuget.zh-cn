---
title: 从 package.config 迁移到 PackageReference 格式
description: 如何将项目从 package.config 管理格式迁移到 PackageReference NuGet 4.0 + 和 VS2017 和.NET Core 2.0 所支持的详细信息
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 09d132aeaf00d2a1d095b9638b455cc23de91f2c
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812875"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="0d606-103">从 packages.config 迁移到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="0d606-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="0d606-104">Visual Studio 2017 版本 15.7年和更高版本支持将项目从迁移[packages.config](./packages-config.md)管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。</span><span class="sxs-lookup"><span data-stu-id="0d606-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="0d606-105">使用 PackageReference 的好处</span><span class="sxs-lookup"><span data-stu-id="0d606-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="0d606-106">**管理在一个位置的所有项目依赖项**:就像项目到项目引用和程序集引用，NuGet 包引用 (使用`PackageReference`节点) 直接在项目文件中托管，而不是使用单独的 packages.config 文件。</span><span class="sxs-lookup"><span data-stu-id="0d606-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="0d606-107">**整洁的顶级依赖项的视图**:与不同的是 packages.config，PackageReference 列出这些项目中直接安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="0d606-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="0d606-108">因此，NuGet 包管理器 UI 和项目文件不会充斥了大量下层依赖项。</span><span class="sxs-lookup"><span data-stu-id="0d606-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="0d606-109">**性能改进**:在使用 PackageReference 时，包中维护*全局包*文件夹 (上所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不在`packages`文件夹中的解决方案。</span><span class="sxs-lookup"><span data-stu-id="0d606-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="0d606-110">因此，PackageReference 更快地执行，并会占用较少的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="0d606-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="0d606-111">**精确地控制对依赖项和内容流**:使用 MSBuild 的现有功能，您可以[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)和选择包引用每个目标框架、 配置、 平台或其他数据透视表。</span><span class="sxs-lookup"><span data-stu-id="0d606-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="0d606-112">**PackageReference 正处于积极开发**:请参阅[PackageReference 问题在 GitHub 上](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="0d606-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="0d606-113">packages.config 不再处于积极开发阶段。</span><span class="sxs-lookup"><span data-stu-id="0d606-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="0d606-114">限制</span><span class="sxs-lookup"><span data-stu-id="0d606-114">Limitations</span></span>

* <span data-ttu-id="0d606-115">NuGet PackageReference 不提供在 Visual Studio 2015 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="0d606-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="0d606-116">只能在 Visual Studio 2017 中可以打开已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="0d606-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="0d606-117">迁移不是当前可用于C++和 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="0d606-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="0d606-118">某些包可能无法与 PackageReference 完全兼容。</span><span class="sxs-lookup"><span data-stu-id="0d606-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="0d606-119">有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="0d606-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="0d606-120">已知问题</span><span class="sxs-lookup"><span data-stu-id="0d606-120">Known Issues</span></span>

1. <span data-ttu-id="0d606-121">`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用</span><span class="sxs-lookup"><span data-stu-id="0d606-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="0d606-122">问题</span><span class="sxs-lookup"><span data-stu-id="0d606-122">Issue</span></span> 
 
<span data-ttu-id="0d606-123">首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。</span><span class="sxs-lookup"><span data-stu-id="0d606-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="0d606-124">这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="0d606-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="0d606-125">解决方法</span><span class="sxs-lookup"><span data-stu-id="0d606-125">Workaround</span></span> 

<span data-ttu-id="0d606-126">执行以下 NuGet 操作之一：</span><span class="sxs-lookup"><span data-stu-id="0d606-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="0d606-127">打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="0d606-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="0d606-128">打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="0d606-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="0d606-129">运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="0d606-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="0d606-130">生成还会触发 NuGet 还原的项目</span><span class="sxs-lookup"><span data-stu-id="0d606-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="0d606-131">现在应能够看到迁移选项。</span><span class="sxs-lookup"><span data-stu-id="0d606-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="0d606-132">请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。</span><span class="sxs-lookup"><span data-stu-id="0d606-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="0d606-133">迁移步骤</span><span class="sxs-lookup"><span data-stu-id="0d606-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="0d606-134">开始迁移之前，Visual Studio 创建项目的备份，可以通过[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。</span><span class="sxs-lookup"><span data-stu-id="0d606-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="0d606-135">打开包含项目使用的解决方案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="0d606-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="0d606-136">在中**解决方案资源管理器**，右键单击**引用**节点或`packages.config`文件，然后选择**将 packages.config 迁移到 PackageReference...** .</span><span class="sxs-lookup"><span data-stu-id="0d606-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="0d606-137">迁移器会分析项目的 NuGet 包引用，并尝试对其进行分类**顶级依赖项**（直接安装的 NuGet 包） 和**可传递依赖项**（已作为顶级包的依赖项安装的包）。</span><span class="sxs-lookup"><span data-stu-id="0d606-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="0d606-138">PackageReference 支持可传递程序包还原，这意味着不必显式安装可传递依赖项动态地解析依赖项。</span><span class="sxs-lookup"><span data-stu-id="0d606-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="0d606-139">（可选）您可以选择将通过选择归类为作为顶级依赖项的可传递依赖项的 NuGet 包**顶级**包的选项。</span><span class="sxs-lookup"><span data-stu-id="0d606-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="0d606-140">此选项会自动设置包包含不间接流动的资产 (中的那些`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`文件夹)，这些标记为开发依赖项 (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="0d606-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="0d606-141">查看任何[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="0d606-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="0d606-142">选择**确定**可开始迁移。</span><span class="sxs-lookup"><span data-stu-id="0d606-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="0d606-143">在迁移结束时，Visual Studio 所提供的备份、 已安装程序包 （顶级依赖项） 的列表，可传递依赖项，作为引用的包的列表和标识的开头的兼容性问题的列表的报表的路径迁移。</span><span class="sxs-lookup"><span data-stu-id="0d606-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="0d606-144">报表将保存到备份文件夹。</span><span class="sxs-lookup"><span data-stu-id="0d606-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="0d606-145">验证解决方案生成并运行。</span><span class="sxs-lookup"><span data-stu-id="0d606-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="0d606-146">如果遇到问题，[在 GitHub 上提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="0d606-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="0d606-147">如何回滚到 packages.config</span><span class="sxs-lookup"><span data-stu-id="0d606-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="0d606-148">关闭已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="0d606-148">Close the migrated project.</span></span>

1. <span data-ttu-id="0d606-149">将项目文件复制并`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 为项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="0d606-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="0d606-150">如果它在项目根目录中存在，请删除 obj 文件夹。</span><span class="sxs-lookup"><span data-stu-id="0d606-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="0d606-151">打开的项目。</span><span class="sxs-lookup"><span data-stu-id="0d606-151">Open the project.</span></span>

1. <span data-ttu-id="0d606-152">打开使用 Package Manager Console**工具 > NuGet 包管理器 > 程序包管理器控制台**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="0d606-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="0d606-153">在控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="0d606-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="0d606-154">迁移后创建的包</span><span class="sxs-lookup"><span data-stu-id="0d606-154">Create a package after migration</span></span>

<span data-ttu-id="0d606-155">迁移完成后，我们建议您添加的引用[nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 包，以及如何将[msbuild 包](../reference/msbuild-targets.md#pack-target)创建包。</span><span class="sxs-lookup"><span data-stu-id="0d606-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="0d606-156">虽然在某些情况下，您可以使用`dotnet.exe pack`而不是`msbuild pack`，不建议。</span><span class="sxs-lookup"><span data-stu-id="0d606-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="0d606-157">包兼容性问题</span><span class="sxs-lookup"><span data-stu-id="0d606-157">Package compatibility issues</span></span>

<span data-ttu-id="0d606-158">PackageReference 中不支持在 packages.config 中受支持的某些方面。</span><span class="sxs-lookup"><span data-stu-id="0d606-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="0d606-159">Migrator 分析，并检测此类问题。</span><span class="sxs-lookup"><span data-stu-id="0d606-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="0d606-160">按预期方式在迁移后，可能不会有一个或多个以下问题的任何包。</span><span class="sxs-lookup"><span data-stu-id="0d606-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="0d606-161">在迁移后安装此包时，将忽略"install.ps1"脚本</span><span class="sxs-lookup"><span data-stu-id="0d606-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="0d606-162">**说明**</span><span class="sxs-lookup"><span data-stu-id="0d606-162">**Description**</span></span> | <span data-ttu-id="0d606-163">利用 PackageReference，安装或卸载包时不执行 install.ps1 和 uninstall.ps1 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="0d606-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="0d606-164">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="0d606-164">**Potential impact**</span></span> | <span data-ttu-id="0d606-165">依赖于这些脚本以配置该目标项目中的某些行为的包可能无法按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="0d606-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="0d606-166">在迁移后安装此包时，"内容"资产不可用</span><span class="sxs-lookup"><span data-stu-id="0d606-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="0d606-167">**说明**</span><span class="sxs-lookup"><span data-stu-id="0d606-167">**Description**</span></span> | <span data-ttu-id="0d606-168">在包中的资产`content`文件夹不支持使用 PackageReference，将被忽略。</span><span class="sxs-lookup"><span data-stu-id="0d606-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="0d606-169">PackageReference 添加了对支持`contentFiles`能够更好地可传递的支持和共享的内容。</span><span class="sxs-lookup"><span data-stu-id="0d606-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="0d606-170">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="0d606-170">**Potential impact**</span></span> | <span data-ttu-id="0d606-171">中的资产`content`不会复制到项目和项目取决于是否存在这些资产的代码需要重构。</span><span class="sxs-lookup"><span data-stu-id="0d606-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="0d606-172">在升级后安装包时，不会应用 XDT 转换</span><span class="sxs-lookup"><span data-stu-id="0d606-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="0d606-173">**说明**</span><span class="sxs-lookup"><span data-stu-id="0d606-173">**Description**</span></span> | <span data-ttu-id="0d606-174">利用 PackageReference 不支持 XDT 转换和`.xdt`安装或卸载包时，将忽略文件。</span><span class="sxs-lookup"><span data-stu-id="0d606-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="0d606-175">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="0d606-175">**Potential impact**</span></span> | <span data-ttu-id="0d606-176">XDT 转换不适用于任何项目的 XML 文件，最常`web.config.install.xdt`并`web.config.uninstall.xdt`，这意味着项目的` web.config`安装或卸载包时不更新文件。</span><span class="sxs-lookup"><span data-stu-id="0d606-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="0d606-177">在迁移后安装此包时，将忽略 lib 根中的程序集</span><span class="sxs-lookup"><span data-stu-id="0d606-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="0d606-178">**说明**</span><span class="sxs-lookup"><span data-stu-id="0d606-178">**Description**</span></span> | <span data-ttu-id="0d606-179">使用 PackageReference，程序集提供的根处`lib`文件夹，但没有目标框架特定子文件夹将被忽略。</span><span class="sxs-lookup"><span data-stu-id="0d606-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="0d606-180">NuGet 查找匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹，并将匹配的程序集安装到项目。</span><span class="sxs-lookup"><span data-stu-id="0d606-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="0d606-181">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="0d606-181">**Potential impact**</span></span> | <span data-ttu-id="0d606-182">不具有匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹的包可能不会像预期在转换后或故障迁移过程的安装</span><span class="sxs-lookup"><span data-stu-id="0d606-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="0d606-183">发现了问题？</span><span class="sxs-lookup"><span data-stu-id="0d606-183">Found an issue?</span></span> <span data-ttu-id="0d606-184">报告它 ！</span><span class="sxs-lookup"><span data-stu-id="0d606-184">Report it!</span></span>

<span data-ttu-id="0d606-185">如果遇到问题的迁移体验，请[NuGet GitHub 存储库中提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="0d606-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
