---
title: 从 package 迁移到 PackageReference 格式
description: 详细介绍了如何将项目从 package 管理格式迁移到 PackageReference (如 NuGet 4.0 + 和 VS2017 和 .NET Core 2.0 所支持)
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 39f260835989cbbcc7293d9db27ac7b2c32debaa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317233"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>从包迁移到 PackageReference

Visual Studio 2017 版本15.7 和更高版本支持将项目从[包 .config](./packages-config.md)管理格式迁移到[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的好处

* **在一个位置管理所有项目依赖项**:与项目到项目的引用和程序集引用一样, NuGet 包引用 ( `PackageReference`使用节点) 直接在项目文件中进行管理, 而不是使用单独的包 .config 文件。
* **顶级依赖项的有序视图**:与包不同, PackageReference 只列出你直接安装在项目中的 NuGet 包。 因此, NuGet 包管理器 UI 和项目文件不会混乱地处理下层依赖项。
* **性能改进**:当使用 PackageReference 时, 包将保留在*全局包*文件夹中 (如[管理全局包和缓存文件夹,](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在解决方案中`packages`的文件夹中所述)。 因此, PackageReference 的执行速度更快, 消耗的磁盘空间更少。
* **精细控制依赖项和内容流**:使用 MSBuild 的现有功能, 可以有[条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition), 并选择每个目标框架、配置、平台或其他透视的包引用。
* **PackageReference 处于积极开发阶段**:请参阅[GitHub 上的 PackageReference 问题](https://aka.ms/nuget-pr-improvements)。 包已不再处于活动状态。

### <a name="limitations"></a>限制

* NuGet PackageReference 在 Visual Studio 2015 及更早版本中不可用。 只能在 Visual Studio 2017 中打开迁移的项目。
* 目前，C++ 和 ASP.NET 项目无法进行迁移。
* 某些包可能与 PackageReference 不完全兼容。 有关详细信息, 请参阅[包兼容性问题](#package-compatibility-issues)。

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
> 在开始迁移之前, Visual Studio 会创建项目的备份, 以便在必要时[回滚到软件包。](#how-to-roll-back-to-packagesconfig)

1. 使用`packages.config`打开包含项目的解决方案。

1. 在**解决方案资源管理器**中, 右键单击 "**引用**" `packages.config`节点或文件, 然后选择 "**将包迁移到 PackageReference**..."。

1. 迁移器分析项目的 NuGet 包引用, 并尝试将它们分类为**顶级依赖项**(你直接安装的 NuGet 包) 和可**传递依赖项**(安装为的包顶层包的依赖项)。

   > [!Note]
   > PackageReference 支持可传递包还原并动态解析依赖项, 这意味着无需显式安装传递依赖项。

1. 可有可无您可以选择将 NuGet 包归类为可传递的依赖项, 方法是选择包的**顶级**选项。 对于包含未按可传递的资产 (在`build` `contentFiles`、 `buildCrossTargeting`、或`analyzers`文件夹中) 和标记为开发依赖项 (`developmentDependency = "true"`) 的资产的包, 将自动设置此选项。

1. 查看任何[包兼容性问题](#package-compatibility-issues)。

1. 选择 **"确定"** 开始迁移。

1. 在迁移结束时, Visual Studio 会提供一个报表, 其中包含指向备份的路径、已安装的包的列表 (顶级依赖项)、被引用为传递依赖项的包列表以及在开始时标识的兼容性问题的列表迁移. 该报表将保存到备份文件夹。

1. 验证解决方案是否已生成并运行。 如果遇到问题, 请[在 GitHub 上发布问题](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回滚到包 .config

1. 关闭已迁移的项目。

1. 将项目文件和`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`为) 复制到项目文件夹。 如果 obj 文件夹位于项目根目录中, 则将其删除。

1. 打开项目。

1. 使用 " **> NuGet 包管理器" > 包管理器控制台**"菜单命令打开包管理器控制台。

1. 在控制台中运行以下命令:

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a>迁移后创建包

迁移完成后, 建议你添加对 t:pack [nuget 包](https://www.nuget.org/packages/nuget.build.tasks.pack)的引用, 然后使用[msbuild](../reference/msbuild-targets.md#pack-target)来创建包 (& e)。 尽管在某些情况下可以使用`dotnet.exe pack` `msbuild -t:pack`而不是, 因此不建议使用。

## <a name="package-compatibility-issues"></a>包兼容性问题

PackageReference 不支持在包中支持的某些方面。 迁移迁移会分析并检测此类问题。 具有以下一个或多个问题的包在迁移后可能不会按预期方式运行。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>如果在迁移之后安装了包, 则将忽略 "install. ps1" 脚本

| | |
| --- | --- |
| **说明** | 使用 PackageReference, 安装或卸载包时, 不会执行 ps1 PowerShell 脚本。 |
| **潜在影响** | 依赖于这些脚本来配置目标项目中的某些行为的包可能不会按预期方式工作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>迁移后, 如果安装了包, 则 "内容" 资产不可用

| | |
| --- | --- |
| **说明** | PackageReference 不支持包的`content`文件夹中的资产, 它们将被忽略。 PackageReference 添加了对`contentFiles`的支持, 以便获得更好的可传递支持和共享内容。  |
| **潜在影响** | 不会`content`将中的资产复制到依赖于这些资产是否需要重构的项目和项目代码中。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>升级后, 如果安装了包, 则不应用 XDT 转换

| | |
| --- | --- |
| **说明** | XDT 转换在 PackageReference 中不受支持`.xdt` , 并且在安装或卸载包时将忽略这些文件。   |
| **潜在影响** | XDT 转换不会应用于任何项目 XML 文件, 最常见的`web.config.install.xdt`是`web.config.uninstall.xdt`和, 这意味着在安装` web.config`或卸载包时不会更新项目的文件。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>当包在迁移后安装后, lib 根中的程序集将被忽略

| | |
| --- | --- |
| **说明** | 使用 PackageReference, 将忽略在`lib`文件夹根目录下的程序集, 而不会忽略特定于目标框架的子文件夹。 NuGet 查找与与项目的目标框架对应的目标框架名字对象 (TFM) 相匹配的子文件夹, 并将匹配的程序集安装到项目中。 |
| **潜在影响** | 不具有与项目的目标框架的目标框架名字对象 (TFM) 匹配的子文件夹的包在迁移期间转换或失败安装后可能不会按预期方式运行 |

## <a name="found-an-issue-report-it"></a>发现问题？ 报告!

如果在迁移过程中遇到问题, 请[在 NuGet GitHub 存储库上发布问题](https://github.com/NuGet/Home/issues/)。
