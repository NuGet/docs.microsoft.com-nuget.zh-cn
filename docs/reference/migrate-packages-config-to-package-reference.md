---
title: 从 package 迁移到 PackageReference 格式
description: 详细介绍了如何将项目从 package 管理格式迁移到 PackageReference (如 NuGet 4.0 + 和 VS2017 和 .NET Core 2.0 所支持)
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: d1c32f4a926f1f688db3ea6a9ca2eed1a21b2dec
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433295"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="e66a9-103">从包迁移到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="e66a9-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="e66a9-104">Visual Studio 2017 版本15.7 和更高版本支持将项目从[包 .config](./packages-config.md)管理格式迁移到[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。</span><span class="sxs-lookup"><span data-stu-id="e66a9-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="e66a9-105">使用 PackageReference 的好处</span><span class="sxs-lookup"><span data-stu-id="e66a9-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="e66a9-106">**在一个位置管理所有项目依赖项**:与项目到项目的引用和程序集引用一样, NuGet 包引用 ( `PackageReference`使用节点) 直接在项目文件中进行管理, 而不是使用单独的包 .config 文件。</span><span class="sxs-lookup"><span data-stu-id="e66a9-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="e66a9-107">**顶级依赖项的有序视图**:与包不同, PackageReference 只列出你直接安装在项目中的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e66a9-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="e66a9-108">因此, NuGet 包管理器 UI 和项目文件不会混乱地处理下层依赖项。</span><span class="sxs-lookup"><span data-stu-id="e66a9-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="e66a9-109">**性能改进**:当使用 PackageReference 时, 包将保留在*全局包*文件夹中 (如[管理全局包和缓存文件夹,](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在解决方案中`packages`的文件夹中所述)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="e66a9-110">因此, PackageReference 的执行速度更快, 消耗的磁盘空间更少。</span><span class="sxs-lookup"><span data-stu-id="e66a9-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="e66a9-111">**精细控制依赖项和内容流**:使用 MSBuild 的现有功能, 可以有[条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition), 并选择每个目标框架、配置、平台或其他透视的包引用。</span><span class="sxs-lookup"><span data-stu-id="e66a9-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="e66a9-112">**PackageReference 处于积极开发阶段**:请参阅[GitHub 上的 PackageReference 问题](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="e66a9-113">包已不再处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="e66a9-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="e66a9-114">限制</span><span class="sxs-lookup"><span data-stu-id="e66a9-114">Limitations</span></span>

* <span data-ttu-id="e66a9-115">NuGet PackageReference 在 Visual Studio 2015 及更早版本中不可用。</span><span class="sxs-lookup"><span data-stu-id="e66a9-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="e66a9-116">只能在 Visual Studio 2017 和更高版本中打开迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="e66a9-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="e66a9-117">目前，C++ 和 ASP.NET 项目无法进行迁移。</span><span class="sxs-lookup"><span data-stu-id="e66a9-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="e66a9-118">某些包可能与 PackageReference 不完全兼容。</span><span class="sxs-lookup"><span data-stu-id="e66a9-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="e66a9-119">有关详细信息, 请参阅[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="e66a9-120">已知问题</span><span class="sxs-lookup"><span data-stu-id="e66a9-120">Known Issues</span></span>

1. <span data-ttu-id="e66a9-121">`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用</span><span class="sxs-lookup"><span data-stu-id="e66a9-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="e66a9-122">问题</span><span class="sxs-lookup"><span data-stu-id="e66a9-122">Issue</span></span> 
 
<span data-ttu-id="e66a9-123">首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。</span><span class="sxs-lookup"><span data-stu-id="e66a9-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="e66a9-124">这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。</span><span class="sxs-lookup"><span data-stu-id="e66a9-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="e66a9-125">解决方法</span><span class="sxs-lookup"><span data-stu-id="e66a9-125">Workaround</span></span> 

<span data-ttu-id="e66a9-126">执行以下 NuGet 操作之一：</span><span class="sxs-lookup"><span data-stu-id="e66a9-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="e66a9-127">打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`</span><span class="sxs-lookup"><span data-stu-id="e66a9-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="e66a9-128">打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="e66a9-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="e66a9-129">运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`</span><span class="sxs-lookup"><span data-stu-id="e66a9-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="e66a9-130">生成还会触发 NuGet 还原的项目</span><span class="sxs-lookup"><span data-stu-id="e66a9-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="e66a9-131">现在应能够看到迁移选项。</span><span class="sxs-lookup"><span data-stu-id="e66a9-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="e66a9-132">请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。</span><span class="sxs-lookup"><span data-stu-id="e66a9-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="e66a9-133">迁移步骤</span><span class="sxs-lookup"><span data-stu-id="e66a9-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="e66a9-134">在开始迁移之前, Visual Studio 会创建项目的备份, 以便在必要时[回滚到软件包。](#how-to-roll-back-to-packagesconfig)</span><span class="sxs-lookup"><span data-stu-id="e66a9-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="e66a9-135">使用`packages.config`打开包含项目的解决方案。</span><span class="sxs-lookup"><span data-stu-id="e66a9-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="e66a9-136">在**解决方案资源管理器**中, 右键单击 "**引用**" `packages.config`节点或文件, 然后选择 "**将包迁移到 PackageReference**..."。</span><span class="sxs-lookup"><span data-stu-id="e66a9-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="e66a9-137">迁移器分析项目的 NuGet 包引用, 并尝试将它们分类为**顶级依赖项**(你直接安装的 NuGet 包) 和可**传递依赖项**(安装为的包顶层包的依赖项)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="e66a9-138">PackageReference 支持可传递包还原并动态解析依赖项, 这意味着无需显式安装传递依赖项。</span><span class="sxs-lookup"><span data-stu-id="e66a9-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="e66a9-139">可有可无您可以选择将 NuGet 包归类为可传递的依赖项, 方法是选择包的**顶级**选项。</span><span class="sxs-lookup"><span data-stu-id="e66a9-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="e66a9-140">对于包含未按可传递的资产 (在`build` `contentFiles`、 `buildCrossTargeting`、或`analyzers`文件夹中) 和标记为开发依赖项 (`developmentDependency = "true"`) 的资产的包, 将自动设置此选项。</span><span class="sxs-lookup"><span data-stu-id="e66a9-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="e66a9-141">查看任何[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="e66a9-142">选择 **"确定"** 开始迁移。</span><span class="sxs-lookup"><span data-stu-id="e66a9-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="e66a9-143">在迁移结束时, Visual Studio 会提供一个报表, 其中包含指向备份的路径、已安装的包的列表 (顶级依赖项)、被引用为传递依赖项的包列表以及在开始时标识的兼容性问题的列表迁移.</span><span class="sxs-lookup"><span data-stu-id="e66a9-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="e66a9-144">该报表将保存到备份文件夹。</span><span class="sxs-lookup"><span data-stu-id="e66a9-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="e66a9-145">验证解决方案是否已生成并运行。</span><span class="sxs-lookup"><span data-stu-id="e66a9-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="e66a9-146">如果遇到问题, 请[在 GitHub 上发布问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="e66a9-147">如何回滚到包 .config</span><span class="sxs-lookup"><span data-stu-id="e66a9-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="e66a9-148">关闭已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="e66a9-148">Close the migrated project.</span></span>

1. <span data-ttu-id="e66a9-149">将项目文件和`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`为) 复制到项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="e66a9-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="e66a9-150">如果 obj 文件夹位于项目根目录中, 则将其删除。</span><span class="sxs-lookup"><span data-stu-id="e66a9-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="e66a9-151">打开项目。</span><span class="sxs-lookup"><span data-stu-id="e66a9-151">Open the project.</span></span>

1. <span data-ttu-id="e66a9-152">使用 " **> NuGet 包管理器" > 包管理器控制台**"菜单命令打开包管理器控制台。</span><span class="sxs-lookup"><span data-stu-id="e66a9-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="e66a9-153">在控制台中运行以下命令:</span><span class="sxs-lookup"><span data-stu-id="e66a9-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="e66a9-154">迁移后创建包</span><span class="sxs-lookup"><span data-stu-id="e66a9-154">Create a package after migration</span></span>

<span data-ttu-id="e66a9-155">迁移完成后, 建议你添加对 t:pack [nuget 包](https://www.nuget.org/packages/nuget.build.tasks.pack)的引用, 然后使用[msbuild](../reference/msbuild-targets.md#pack-target)来创建包 (& e)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="e66a9-156">尽管在某些情况下可以使用`dotnet.exe pack` `msbuild -t:pack`而不是, 因此不建议使用。</span><span class="sxs-lookup"><span data-stu-id="e66a9-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="e66a9-157">包兼容性问题</span><span class="sxs-lookup"><span data-stu-id="e66a9-157">Package compatibility issues</span></span>

<span data-ttu-id="e66a9-158">PackageReference 不支持在包中支持的某些方面。</span><span class="sxs-lookup"><span data-stu-id="e66a9-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="e66a9-159">迁移迁移会分析并检测此类问题。</span><span class="sxs-lookup"><span data-stu-id="e66a9-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="e66a9-160">具有以下一个或多个问题的包在迁移后可能不会按预期方式运行。</span><span class="sxs-lookup"><span data-stu-id="e66a9-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="e66a9-161">如果在迁移之后安装了包, 则将忽略 "install. ps1" 脚本</span><span class="sxs-lookup"><span data-stu-id="e66a9-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e66a9-162">**说明**</span><span class="sxs-lookup"><span data-stu-id="e66a9-162">**Description**</span></span> | <span data-ttu-id="e66a9-163">使用 PackageReference, 安装或卸载包时, 不会执行 ps1 PowerShell 脚本。</span><span class="sxs-lookup"><span data-stu-id="e66a9-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="e66a9-164">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="e66a9-164">**Potential impact**</span></span> | <span data-ttu-id="e66a9-165">依赖于这些脚本来配置目标项目中的某些行为的包可能不会按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="e66a9-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="e66a9-166">迁移后, 如果安装了包, 则 "内容" 资产不可用</span><span class="sxs-lookup"><span data-stu-id="e66a9-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e66a9-167">**说明**</span><span class="sxs-lookup"><span data-stu-id="e66a9-167">**Description**</span></span> | <span data-ttu-id="e66a9-168">PackageReference 不支持包的`content`文件夹中的资产, 它们将被忽略。</span><span class="sxs-lookup"><span data-stu-id="e66a9-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="e66a9-169">PackageReference 添加了对`contentFiles`的支持, 以便获得更好的可传递支持和共享内容。</span><span class="sxs-lookup"><span data-stu-id="e66a9-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="e66a9-170">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="e66a9-170">**Potential impact**</span></span> | <span data-ttu-id="e66a9-171">不会`content`将中的资产复制到依赖于这些资产是否需要重构的项目和项目代码中。</span><span class="sxs-lookup"><span data-stu-id="e66a9-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="e66a9-172">升级后, 如果安装了包, 则不应用 XDT 转换</span><span class="sxs-lookup"><span data-stu-id="e66a9-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e66a9-173">**说明**</span><span class="sxs-lookup"><span data-stu-id="e66a9-173">**Description**</span></span> | <span data-ttu-id="e66a9-174">XDT 转换在 PackageReference 中不受支持`.xdt` , 并且在安装或卸载包时将忽略这些文件。</span><span class="sxs-lookup"><span data-stu-id="e66a9-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="e66a9-175">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="e66a9-175">**Potential impact**</span></span> | <span data-ttu-id="e66a9-176">XDT 转换不会应用于任何项目 XML 文件, 最常见的`web.config.install.xdt`是`web.config.uninstall.xdt`和, 这意味着在安装` web.config`或卸载包时不会更新项目的文件。</span><span class="sxs-lookup"><span data-stu-id="e66a9-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="e66a9-177">当包在迁移后安装后, lib 根中的程序集将被忽略</span><span class="sxs-lookup"><span data-stu-id="e66a9-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e66a9-178">**说明**</span><span class="sxs-lookup"><span data-stu-id="e66a9-178">**Description**</span></span> | <span data-ttu-id="e66a9-179">使用 PackageReference, 将忽略在`lib`文件夹根目录下的程序集, 而不会忽略特定于目标框架的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="e66a9-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="e66a9-180">NuGet 查找与与项目的目标框架对应的目标框架名字对象 (TFM) 相匹配的子文件夹, 并将匹配的程序集安装到项目中。</span><span class="sxs-lookup"><span data-stu-id="e66a9-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="e66a9-181">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="e66a9-181">**Potential impact**</span></span> | <span data-ttu-id="e66a9-182">不具有与项目的目标框架的目标框架名字对象 (TFM) 匹配的子文件夹的包在迁移期间转换或失败安装后可能不会按预期方式运行</span><span class="sxs-lookup"><span data-stu-id="e66a9-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="e66a9-183">发现问题？</span><span class="sxs-lookup"><span data-stu-id="e66a9-183">Found an issue?</span></span> <span data-ttu-id="e66a9-184">报告!</span><span class="sxs-lookup"><span data-stu-id="e66a9-184">Report it!</span></span>

<span data-ttu-id="e66a9-185">如果在迁移过程中遇到问题, 请[在 NuGet GitHub 存储库上发布问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="e66a9-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
