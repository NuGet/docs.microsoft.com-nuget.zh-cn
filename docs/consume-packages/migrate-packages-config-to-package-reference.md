---
title: 从 package.config 迁移到 PackageReference 格式
description: 详细介绍了如何将项目从 package.config 管理格式迁移到 NuGet 4.0+、VS2017 以及 .NET Core 2.0 支持的 PackageReference
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231262"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>从 packages.config 迁移到 PackageReference

Visual Studio 2017 版本 15.7 及更高版本支持将项目从 [packages.config](../reference/packages-config.md) 管理格式迁移到 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的好处

* **在一个位置管理所有项目依赖项**：与项目到项目的引用和程序集引用一样，NuGet 包引用（使用 `PackageReference` 节点）直接在项目文件中进行管理，而不是使用单独的 packages.config 文件进行管理。
* **顶级依赖项的有序视图**：与 packages.config 不同，PackageReference 仅列出那些直接安装在项目中的 NuGet 包。 因此，NuGet 包管理器 UI 和项目文件不会与低级依赖项混在一起。
* **性能改进**：使用 PackageReference 时，包保留在 global-packages  文件夹中（而不是解决方案中的 `packages` 文件夹中），如[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)中所述。 因此，PackageReference 的执行速度更快，但占用的磁盘空间更少。
* **更好地控制依赖项和内容流**：使用 MSBuild 的现有功能可以[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)，并选择每个目标框架、配置、平台或其他透视的包引用。
* **PackageReference 正处于积极开发阶段**：请参阅 [GitHub 上的 PackageReference 问题](https://aka.ms/nuget-pr-improvements)。 packages.config 不再处于积极开发阶段。

### <a name="limitations"></a>限制

* NuGet PackageReference 在 Visual Studio 2015 及更早版本中不可用。 只能在 Visual Studio 2017 及更高版本中打开已迁移的项目。
* 目前，C++ 和 ASP.NET 项目无法进行迁移。
* 某些包可能与 PackageReference 不完全兼容。 有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。

此外，PackageReferences 的工作原理与 packages.config 相比存在一些差异。例如，PackageReference 不支持[约束升级版本](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)，但添加了对[可变版本](../consume-packages/package-references-in-project-files.md#floating-versions)的支持。

### <a name="known-issues"></a>已知问题

1. `Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用 

#### <a name="issue"></a>问题 
 
首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。 这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。 

#### <a name="workaround"></a>解决方法 

执行以下 NuGet 操作之一： 
* 打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...` 
* 打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console` 
* 运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages` 
* 生成还会触发 NuGet 还原的项目 

现在应能够看到迁移选项。 请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。 

## <a name="migration-steps"></a>迁移步骤

> [!Note]
> 在开始迁移之前，Visual Studio 会创建项目的备份，以便在必要时[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)。

1. 使用 `packages.config` 打开包含项目的解决方案。

1. 在“解决方案资源管理器”中，右键单击“引用”节点或 `packages.config` 文件，然后选择“将 packages.config 迁移到 PackageReference...”    。

1. 迁移程序将分析项目的 NuGet 包引用并尝试将它们分类为“顶级依赖项”  （直接安装的 NuGet 包）和  “可传递的依赖项”（作为顶级包的依赖项安装的包）。

   > [!Note]
   > PackageReference 支持可传递包还原并动态解析依赖项，这意味着无需显式安装可传递的依赖项。

1. （可选）可以选择将分类为可传递的依赖项的 NuGet 包视为顶级依赖项，方法是为包选择  “顶级”选项。 对于包含不以可传递的方式流式传输的资产（`build`、`buildCrossTargeting`、`contentFiles` 或 `analyzers` 文件夹中的资产）以及标记为开发依赖项 (`developmentDependency = "true"`) 的资产的包，将自动设置此选项。

1. 查看任何[包兼容性问题](#package-compatibility-issues)。

1. 选择“确定”  ，开始迁移。

1. 迁移结束时，Visual Studio 会提供一个报表，其中包含指向备份的路径、已安装包的列表（顶级依赖项）、作为可传递的依赖项引用的包的列表以及在开始迁移时确定的兼容性问题的列表。 该报表将保存到备份文件夹。

1. 验证解决方案是否生成并运行。 如果遇到问题，请[在 GitHub 上提出问题](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回滚到 packages.config

1. 关闭已迁移的项目。

1. 将项目文件和 `packages.config` 从备份（通常为 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`）复制到项目文件夹。 如果项目根目录中存在 obj 文件夹，则删除该文件夹。

1. 打开项目。

1. 使用“工具”>“NuGet 包管理器”>“包管理器控制台”菜单命令打开包管理器控制台  。

1. 在控制台中运行以下命令：

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>迁移后创建包

迁移完成后，建议你添加对 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 包的引用，然后使用 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) 来创建包。 尽管在某些情况下可以使用 `dotnet.exe pack` 而不是 `msbuild -t:pack`，但不建议使用。

## <a name="package-compatibility-issues"></a>包兼容性问题

PackageReference 不支持 packages.config 支持的某些方面。 迁移程序将分析并检测此类问题。 具有以下一个或多个问题的任何包在迁移后可能无法按预期方式工作。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>如果在迁移后安装了包，则将忽略“install.ps1”脚本

| | |
| --- | --- |
| **说明** | 借助 PackageReference，安装或卸载包时不会执行 install.ps1 和 uninstall.ps1 PowerShell 脚本。 |
| **潜在影响** | 依赖于这些脚本来配置目标项目中的某些行为的包可能无法按预期方式工作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>如果在迁移后安装了包，则“内容”资产不可用

| | |
| --- | --- |
| **说明** | 包的 `content` 文件夹中的资产不受 PackageReference 支持，并且将被忽略。 PackageReference 添加了对 `contentFiles` 的支持，以便获得更好的可传递支持和共享内容。  |
| **潜在影响** | `content` 中的资产不会复制到项目中，依赖于这些资产的项目代码需要重构。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>如果在升级后安装了包，则不会应用 XDT 转换

| | |
| --- | --- |
| **说明** | PackageReference 不支持 XDT 转换，因此在安装或卸载包时将忽略 `.xdt` 文件。   |
| **潜在影响** | XDT 转换不会应用于任何项目 XML 文件（最常见的是 `web.config.install.xdt` 和 `web.config.uninstall.xdt`），这意味着在安装或卸载包时不会更新项目的 ` web.config` 文件。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>如果在迁移后安装了包，则将忽略 lib 根目录中的程序集

| | |
| --- | --- |
| **说明** | 借助 PackageReference，将忽略无目标框架特定子文件夹的 `lib` 文件夹的根目录中的程序集。 NuGet 会查找与对应于项目的目标框架的目标框架名字对象 (TFM) 相匹配的子文件夹，并将匹配的程序集安装到项目中。 |
| **潜在影响** | 没有与对应于项目的目标框架的目标框架名字对象 (TFM) 相匹配的子文件夹的包在迁移期间转换或安装失败后可能无法按预期方式工作 |

## <a name="found-an-issue-report-it"></a>如果发现错误， 请将其报告！

如果在迁移过程中遇到问题，请[在 NuGet GitHub 存储库上提出问题](https://github.com/NuGet/Home/issues/)。
