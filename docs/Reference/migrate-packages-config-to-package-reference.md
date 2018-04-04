---
title: 从 package.config 迁移到 PackageReference 格式 |Microsoft 文档
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: 有关如何将从 package.config 管理格式的项目迁移到 PackageReference NuGet 4.0 + 和 VS2017 和.NET 核心 2.0 所支持的详细信息
keywords: NuGet 迁移器迁移、 包的引用，项目文件，PackageReference，packages.config VS2017、 Visual Studio 2017、 NuGet 4、.NET 核心 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="86d79-104">将从 packages.config 迁移到 PackageReference</span><span class="sxs-lookup"><span data-stu-id="86d79-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="86d79-105">Visual Studio 2017 版本 15.7年预览版 3年和更高版本中迁移从项目的支持[packages.config](./packages-config.md)管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。</span><span class="sxs-lookup"><span data-stu-id="86d79-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="86d79-106">使用 PackageReference 的好处</span><span class="sxs-lookup"><span data-stu-id="86d79-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="86d79-107">**管理在一个位置的所有项目依赖项**： 一样项目到项目引用和程序集引用，NuGet 包引用 (使用`PackageReference`节点) 直接在项目文件中管理，而不是使用单独packages.config 文件。</span><span class="sxs-lookup"><span data-stu-id="86d79-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="86d79-108">**顶级依赖项的整洁的视图**： 与 packages.config，不同 PackageReference 列出这些项目中直接安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="86d79-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="86d79-109">因此，NuGet 包管理器 UI 和项目文件不杂乱具有低级别依赖项。</span><span class="sxs-lookup"><span data-stu-id="86d79-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="86d79-110">**性能改进**： 如果使用 PackageReference，包将保留在*全局包*文件夹 (如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在`packages`解决方案中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="86d79-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="86d79-111">因此，PackageReference 执行得更快，并使用较少的磁盘空间。</span><span class="sxs-lookup"><span data-stu-id="86d79-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="86d79-112">**微调对依赖关系和内容的流控制**： 使用 MSBuild 的现有功能允许你为[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)选择每个目标框架的包引用和配置，平台或其他透视。</span><span class="sxs-lookup"><span data-stu-id="86d79-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="86d79-113">**PackageReference 是进行活动开发**： 请参阅[PackageReference 发出在 GitHub 上](https://aka.ms/nuget-pr-improvements)。</span><span class="sxs-lookup"><span data-stu-id="86d79-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="86d79-114">packages.config 不再进行活动开发。</span><span class="sxs-lookup"><span data-stu-id="86d79-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="86d79-115">限制</span><span class="sxs-lookup"><span data-stu-id="86d79-115">Limitations</span></span>

* <span data-ttu-id="86d79-116">NuGet PackageReference 不位于 Visual Studio 2015 及更早版本。</span><span class="sxs-lookup"><span data-stu-id="86d79-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="86d79-117">只能在 Visual Studio 2017 中，可以打开迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="86d79-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="86d79-118">迁移不是当前可用于 c + + 和 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="86d79-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="86d79-119">某些包可能无法与 PackageReference 完全兼容。</span><span class="sxs-lookup"><span data-stu-id="86d79-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="86d79-120">有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="86d79-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="86d79-121">迁移步骤</span><span class="sxs-lookup"><span data-stu-id="86d79-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="86d79-122">开始迁移之前，Visual Studio 将创建该项目的备份以使您能够[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。</span><span class="sxs-lookup"><span data-stu-id="86d79-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="86d79-123">打开包含项目使用的解决方案`packages.config`。</span><span class="sxs-lookup"><span data-stu-id="86d79-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="86d79-124">在**解决方案资源管理器**，右键单击**引用**节点或`packages.config`文件，然后选择**将 packages.config 迁移到 PackageReference...**.</span><span class="sxs-lookup"><span data-stu-id="86d79-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="86d79-125">迁移器分析项目的 NuGet 包引用，并尝试对其进行分类入**顶级依赖项**（NuGet 包你安装目录） 和**可传递的依赖关系**（顶级包的依赖关系中已安装的包）。</span><span class="sxs-lookup"><span data-stu-id="86d79-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="86d79-126">PackageReference 支持可传递的程序包还原并解析依赖项动态，这意味着需要显式安装可传递的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="86d79-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="86d79-127">（可选）你可以选择将通过选择归类为传递的依赖关系作为顶级依赖项 NuGet 包**顶级**包的选项。</span><span class="sxs-lookup"><span data-stu-id="86d79-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="86d79-128">包含不间接流的资产的包将自动设置此选项 (中的那些`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`文件夹)，这些标记为开发依赖项 (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="86d79-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="86d79-129">查看任何[包兼容性问题](#package-compatibility-issues)。</span><span class="sxs-lookup"><span data-stu-id="86d79-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="86d79-130">选择**确定**可开始迁移。</span><span class="sxs-lookup"><span data-stu-id="86d79-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="86d79-131">在迁移结束时，Visual Studio 具有路径的报表提供备份、 安装程序包 （顶级依赖项） 的列表，可传递的依赖关系引用的包的列表和列表的开头所述的兼容性问题迁移。</span><span class="sxs-lookup"><span data-stu-id="86d79-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="86d79-132">报表保存到备份文件夹。</span><span class="sxs-lookup"><span data-stu-id="86d79-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="86d79-133">验证解决方案将生成并运行。</span><span class="sxs-lookup"><span data-stu-id="86d79-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="86d79-134">如果你遇到问题， [GitHub 上的文件出现问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="86d79-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="86d79-135">如何回滚到 packages.config</span><span class="sxs-lookup"><span data-stu-id="86d79-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="86d79-136">关闭已迁移的项目。</span><span class="sxs-lookup"><span data-stu-id="86d79-136">Close the migrated project.</span></span>

1. <span data-ttu-id="86d79-137">将项目文件复制和`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 到项目文件夹。</span><span class="sxs-lookup"><span data-stu-id="86d79-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="86d79-138">打开项目。</span><span class="sxs-lookup"><span data-stu-id="86d79-138">Open the project.</span></span>

1. <span data-ttu-id="86d79-139">打开程序包管理器控制台使用**工具 > NuGet 包管理器 > 程序包管理器控制台**菜单命令。</span><span class="sxs-lookup"><span data-stu-id="86d79-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="86d79-140">在控制台中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="86d79-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="86d79-141">包兼容性问题</span><span class="sxs-lookup"><span data-stu-id="86d79-141">Package compatibility issues</span></span>

<span data-ttu-id="86d79-142">PackageReference 中不支持在 packages.config 中受支持的某些方面。</span><span class="sxs-lookup"><span data-stu-id="86d79-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="86d79-143">迁移器分析，并检测到此类问题。</span><span class="sxs-lookup"><span data-stu-id="86d79-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="86d79-144">按预期在迁移后，可能无法正常工作的任何包都具有一个或多个以下的问题。</span><span class="sxs-lookup"><span data-stu-id="86d79-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="86d79-145">在迁移后安装此包时，将忽略"install.ps1"脚本</span><span class="sxs-lookup"><span data-stu-id="86d79-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="86d79-146">**说明**</span><span class="sxs-lookup"><span data-stu-id="86d79-146">**Description**</span></span> | <span data-ttu-id="86d79-147">与 PackageReference，install.ps1，uninstall.ps1 PowerShell 脚本将不安装或卸载程序包时执行。</span><span class="sxs-lookup"><span data-stu-id="86d79-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="86d79-148">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="86d79-148">**Potential impact**</span></span> | <span data-ttu-id="86d79-149">包依赖于这些脚本以配置目标项目中的某些行为可能不会按预期工作。</span><span class="sxs-lookup"><span data-stu-id="86d79-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="86d79-150">在迁移后安装此包时，"内容"资产不可用</span><span class="sxs-lookup"><span data-stu-id="86d79-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="86d79-151">**说明**</span><span class="sxs-lookup"><span data-stu-id="86d79-151">**Description**</span></span> | <span data-ttu-id="86d79-152">包中的资产`content`文件夹不支持 PackageReference 和将被忽略。</span><span class="sxs-lookup"><span data-stu-id="86d79-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="86d79-153">PackageReference 增加了对支持`contentFiles`能够更好地可传递的支持和共享的内容。</span><span class="sxs-lookup"><span data-stu-id="86d79-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="86d79-154">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="86d79-154">**Potential impact**</span></span> | <span data-ttu-id="86d79-155">中的资产`content`不会复制到项目和项目取决于这些资产是否存在的代码需要重构。</span><span class="sxs-lookup"><span data-stu-id="86d79-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="86d79-156">升级之后安装此包时，不会应用 XDT 转换</span><span class="sxs-lookup"><span data-stu-id="86d79-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="86d79-157">**说明**</span><span class="sxs-lookup"><span data-stu-id="86d79-157">**Description**</span></span> | <span data-ttu-id="86d79-158">XDT 转换不支持 PackageReference 和`.xdt`安装或卸载程序包时忽略文件。</span><span class="sxs-lookup"><span data-stu-id="86d79-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="86d79-159">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="86d79-159">**Potential impact**</span></span> | <span data-ttu-id="86d79-160">XDT 转换不会应用与任何项目的 XML 文件，通常情况下，`web.config.install.xdt`和`web.config.uninstall.xdt`，这意味着项目的` web.config`安装或卸载该包时，不会更新文件。</span><span class="sxs-lookup"><span data-stu-id="86d79-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="86d79-161">在迁移后安装此包时，将忽略 lib 根中的程序集</span><span class="sxs-lookup"><span data-stu-id="86d79-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="86d79-162">**说明**</span><span class="sxs-lookup"><span data-stu-id="86d79-162">**Description**</span></span> | <span data-ttu-id="86d79-163">PackageReference，与程序集存在根目录下的`lib`而无需的目标 framework 的特定子文件夹的文件夹将被忽略。</span><span class="sxs-lookup"><span data-stu-id="86d79-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="86d79-164">NuGet 查找匹配的目标框架名字对象 (TFM) 的项目的目标框架所对应的子文件夹，并在项目中安装匹配的程序集。</span><span class="sxs-lookup"><span data-stu-id="86d79-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="86d79-165">**潜在影响**</span><span class="sxs-lookup"><span data-stu-id="86d79-165">**Potential impact**</span></span> | <span data-ttu-id="86d79-166">没有匹配的目标框架名字对象 (TFM) 的项目的目标框架所对应的子文件夹的包可能不会像预期的那样在转换后或失败迁移期间的安装</span><span class="sxs-lookup"><span data-stu-id="86d79-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="86d79-167">发现了一个问题？</span><span class="sxs-lookup"><span data-stu-id="86d79-167">Found an issue?</span></span> <span data-ttu-id="86d79-168">报告它 ！</span><span class="sxs-lookup"><span data-stu-id="86d79-168">Report it!</span></span>

<span data-ttu-id="86d79-169">如果你遇到迁移体验问题，请[NuGet GitHub 存储库上的文件出现问题](https://github.com/NuGet/Home/issues/)。</span><span class="sxs-lookup"><span data-stu-id="86d79-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
