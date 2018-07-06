---
title: 从 package.config 迁移到 PackageReference 格式
description: 如何将项目从 package.config 管理格式迁移到 PackageReference NuGet 4.0 + 和 VS2017 和.NET Core 2.0 所支持的详细信息
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 1ca97e1c2dfba876aefe6b06eab10def67b8d848
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843389"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="11b0b-103">从 packages.config 迁移到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="11b0b-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="11b0b-104">Visual Studio 2017 版本 15.7年和更高版本支持将项目从迁移[packages.config](./packages-config.md)管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。</span><span class="sxs-lookup"><span data-stu-id="11b0b-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="11b0b-105">使用 PackageReference 的好处</span><span class="sxs-lookup"><span data-stu-id="11b0b-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="11b0b-106">**管理在一个位置的所有项目依赖项**： 一样项目到项目引用和程序集引用，NuGet 包引用 (使用`PackageReference`节点) 直接在项目文件中托管，而不是使用单独的packages.config 文件。</span><span class="sxs-lookup"><span data-stu-id="11b0b-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="11b0b-107">**整洁的顶级依赖项的视图**： 与 packages.config，不同 PackageReference 列出这些项目中直接安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="11b0b-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="11b0b-108">因此，NuGet 包管理器 UI 和项目文件不会充斥了大量下层依赖项。</span><span class="sxs-lookup"><span data-stu-id="11b0b-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="11b0b-109">**性能改进**： 在使用 PackageReference 时，包都保留在*全局包*文件夹 (如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不在`packages`解决方案中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="11b0b-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="11b0b-110">因此，PackageReference 更快地执行，并会占用较少的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="11b0b-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="11b0b-111">**精确地控制对依赖项和内容流**： 使用 MSBuild 的现有功能，您可以[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)选择每个目标框架的包引用和配置，平台或其他数据透视表。</span><span class="sxs-lookup"><span data-stu-id="11b0b-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="11b0b-112">**PackageReference 正处于积极开发**： 请参阅[在 GitHub 上发出 PackageReference](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="11b0b-113">packages.config 不再处于积极开发阶段。</span><span class="sxs-lookup"><span data-stu-id="11b0b-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="11b0b-114">限制</span><span class="sxs-lookup"><span data-stu-id="11b0b-114">Limitations</span></span>

* <span data-ttu-id="11b0b-115">NuGet PackageReference 不提供在 Visual Studio 2015 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="11b0b-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="11b0b-116">只能在 Visual Studio 2017 中可以打开已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="11b0b-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="11b0b-117">迁移不是当前可用于 c + + 和 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="11b0b-117">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="11b0b-118">某些包可能无法与 PackageReference 完全兼容。</span><span class="sxs-lookup"><span data-stu-id="11b0b-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="11b0b-119">有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="11b0b-120">已知问题</span><span class="sxs-lookup"><span data-stu-id="11b0b-120">Known Issues</span></span>

1. <span data-ttu-id="11b0b-121">`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用</span><span class="sxs-lookup"><span data-stu-id="11b0b-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="11b0b-122">问题</span><span class="sxs-lookup"><span data-stu-id="11b0b-122">Issue</span></span> 
 
<span data-ttu-id="11b0b-123">首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。</span><span class="sxs-lookup"><span data-stu-id="11b0b-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="11b0b-124">这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="11b0b-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="11b0b-125">解决方法</span><span class="sxs-lookup"><span data-stu-id="11b0b-125">Workaround</span></span> 

<span data-ttu-id="11b0b-126">执行以下 NuGet 操作之一：</span><span class="sxs-lookup"><span data-stu-id="11b0b-126">Peform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="11b0b-127">打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="11b0b-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="11b0b-128">打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="11b0b-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="11b0b-129">运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="11b0b-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="11b0b-130">生成还会触发 NuGet 还原的项目</span><span class="sxs-lookup"><span data-stu-id="11b0b-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="11b0b-131">现在应能够看到迁移选项。</span><span class="sxs-lookup"><span data-stu-id="11b0b-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="11b0b-132">请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。</span><span class="sxs-lookup"><span data-stu-id="11b0b-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="11b0b-133">迁移步骤</span><span class="sxs-lookup"><span data-stu-id="11b0b-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="11b0b-134">开始迁移之前，Visual Studio 创建项目的备份，可以通过[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。</span><span class="sxs-lookup"><span data-stu-id="11b0b-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="11b0b-135">打开包含项目使用的解决方案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="11b0b-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="11b0b-136">在中**解决方案资源管理器**，右键单击**引用**节点或`packages.config`文件，然后选择**将 packages.config 迁移到 PackageReference...**.</span><span class="sxs-lookup"><span data-stu-id="11b0b-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="11b0b-137">迁移器会分析项目的 NuGet 包引用，并尝试对其进行分类**顶级依赖项**（NuGet 包已安装目录） 和**可传递依赖项**（已作为顶级包的依赖项安装的包）。</span><span class="sxs-lookup"><span data-stu-id="11b0b-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="11b0b-138">PackageReference 支持可传递程序包还原，这意味着不必显式安装可传递依赖项动态地解析依赖项。</span><span class="sxs-lookup"><span data-stu-id="11b0b-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="11b0b-139">（可选）您可以选择将通过选择归类为作为顶级依赖项的可传递依赖项的 NuGet 包**顶级**包的选项。</span><span class="sxs-lookup"><span data-stu-id="11b0b-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="11b0b-140">此选项会自动设置包包含不间接流动的资产 (中的那些`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`文件夹)，这些标记为开发依赖项 (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="11b0b-141">查看任何[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="11b0b-142">选择**确定**可开始迁移。</span><span class="sxs-lookup"><span data-stu-id="11b0b-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="11b0b-143">在迁移结束时，Visual Studio 所提供的备份、 已安装程序包 （顶级依赖项） 的列表，可传递依赖项，作为引用的包的列表和标识的开头的兼容性问题的列表的报表的路径迁移。</span><span class="sxs-lookup"><span data-stu-id="11b0b-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="11b0b-144">报表将保存到备份文件夹。</span><span class="sxs-lookup"><span data-stu-id="11b0b-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="11b0b-145">验证解决方案生成并运行。</span><span class="sxs-lookup"><span data-stu-id="11b0b-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="11b0b-146">如果遇到问题，[在 GitHub 上提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="11b0b-147">如何回滚到 packages.config</span><span class="sxs-lookup"><span data-stu-id="11b0b-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="11b0b-148">关闭已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="11b0b-148">Close the migrated project.</span></span>

1. <span data-ttu-id="11b0b-149">将项目文件复制并`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 为项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="11b0b-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="11b0b-150">如果它在项目根目录中存在，请删除 obj 文件夹。</span><span class="sxs-lookup"><span data-stu-id="11b0b-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="11b0b-151">打开的项目。</span><span class="sxs-lookup"><span data-stu-id="11b0b-151">Open the project.</span></span>

1. <span data-ttu-id="11b0b-152">打开使用 Package Manager Console**工具 > NuGet 包管理器 > 程序包管理器控制台**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="11b0b-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="11b0b-153">在控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="11b0b-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="11b0b-154">包兼容性问题</span><span class="sxs-lookup"><span data-stu-id="11b0b-154">Package compatibility issues</span></span>

<span data-ttu-id="11b0b-155">PackageReference 中不支持在 packages.config 中受支持的某些方面。</span><span class="sxs-lookup"><span data-stu-id="11b0b-155">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="11b0b-156">Migrator 分析，并检测此类问题。</span><span class="sxs-lookup"><span data-stu-id="11b0b-156">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="11b0b-157">按预期方式在迁移后，可能不会有一个或多个以下问题的任何包。</span><span class="sxs-lookup"><span data-stu-id="11b0b-157">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="11b0b-158">在迁移后安装此包时，将忽略"install.ps1"脚本</span><span class="sxs-lookup"><span data-stu-id="11b0b-158">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11b0b-159">**说明**</span><span class="sxs-lookup"><span data-stu-id="11b0b-159">**Description**</span></span> | <span data-ttu-id="11b0b-160">利用 PackageReference，安装或卸载包时不执行 install.ps1 和 uninstall.ps1 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="11b0b-160">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="11b0b-161">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="11b0b-161">**Potential impact**</span></span> | <span data-ttu-id="11b0b-162">依赖于这些脚本以配置该目标项目中的某些行为的包可能无法按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="11b0b-162">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="11b0b-163">在迁移后安装此包时，"内容"资产不可用</span><span class="sxs-lookup"><span data-stu-id="11b0b-163">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11b0b-164">**说明**</span><span class="sxs-lookup"><span data-stu-id="11b0b-164">**Description**</span></span> | <span data-ttu-id="11b0b-165">在包中的资产`content`文件夹不支持使用 PackageReference，将被忽略。</span><span class="sxs-lookup"><span data-stu-id="11b0b-165">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="11b0b-166">PackageReference 添加了对支持`contentFiles`能够更好地可传递的支持和共享的内容。</span><span class="sxs-lookup"><span data-stu-id="11b0b-166">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="11b0b-167">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="11b0b-167">**Potential impact**</span></span> | <span data-ttu-id="11b0b-168">中的资产`content`不会复制到项目和项目取决于是否存在这些资产的代码需要重构。</span><span class="sxs-lookup"><span data-stu-id="11b0b-168">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="11b0b-169">在升级后安装包时，不会应用 XDT 转换</span><span class="sxs-lookup"><span data-stu-id="11b0b-169">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11b0b-170">**说明**</span><span class="sxs-lookup"><span data-stu-id="11b0b-170">**Description**</span></span> | <span data-ttu-id="11b0b-171">利用 PackageReference 不支持 XDT 转换和`.xdt`安装或卸载包时，将忽略文件。</span><span class="sxs-lookup"><span data-stu-id="11b0b-171">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="11b0b-172">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="11b0b-172">**Potential impact**</span></span> | <span data-ttu-id="11b0b-173">XDT 转换不适用于任何项目的 XML 文件，最常`web.config.install.xdt`并`web.config.uninstall.xdt`，这意味着项目的` web.config`安装或卸载包时不更新文件。</span><span class="sxs-lookup"><span data-stu-id="11b0b-173">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="11b0b-174">在迁移后安装此包时，将忽略 lib 根中的程序集</span><span class="sxs-lookup"><span data-stu-id="11b0b-174">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11b0b-175">**说明**</span><span class="sxs-lookup"><span data-stu-id="11b0b-175">**Description**</span></span> | <span data-ttu-id="11b0b-176">使用 PackageReference，程序集提供的根处`lib`文件夹，但没有目标框架特定子文件夹将被忽略。</span><span class="sxs-lookup"><span data-stu-id="11b0b-176">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="11b0b-177">NuGet 查找匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹，并将匹配的程序集安装到项目。</span><span class="sxs-lookup"><span data-stu-id="11b0b-177">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="11b0b-178">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="11b0b-178">**Potential impact**</span></span> | <span data-ttu-id="11b0b-179">不具有匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹的包可能不会像预期在转换后或故障迁移过程的安装</span><span class="sxs-lookup"><span data-stu-id="11b0b-179">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="11b0b-180">发现了问题？</span><span class="sxs-lookup"><span data-stu-id="11b0b-180">Found an issue?</span></span> <span data-ttu-id="11b0b-181">报告它 ！</span><span class="sxs-lookup"><span data-stu-id="11b0b-181">Report it!</span></span>

<span data-ttu-id="11b0b-182">如果遇到问题的迁移体验，请[NuGet GitHub 存储库中提出问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="11b0b-182">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
