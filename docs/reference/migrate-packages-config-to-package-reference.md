---
title: 从 package.config 迁移到 PackageReference 格式
description: 如何将项目从 package.config 管理格式迁移到 PackageReference NuGet 4.0 + 和 VS2017 和.NET Core 2.0 所支持的详细信息
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: b05192038bff071ca7a5b8f2e0f735696d09bef6
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508265"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>从 packages.config 迁移到 PackageReference

Visual Studio 2017 版本 15.7年和更高版本支持将项目从迁移[packages.config](./packages-config.md)管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的好处

* **管理在一个位置的所有项目依赖项**： 一样项目到项目引用和程序集引用，NuGet 包引用 (使用`PackageReference`节点) 直接在项目文件中托管，而不是使用单独的packages.config 文件。
* **整洁的顶级依赖项的视图**： 与 packages.config，不同 PackageReference 列出这些项目中直接安装的 NuGet 包。 因此，NuGet 包管理器 UI 和项目文件不会充斥了大量下层依赖项。
* **性能改进**： 在使用 PackageReference 时，包都保留在*全局包*文件夹 (如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不在`packages`解决方案中的文件夹。 因此，PackageReference 更快地执行，并会占用较少的磁盘空间。
* **精确地控制对依赖项和内容流**： 使用 MSBuild 的现有功能，您可以[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)选择每个目标框架的包引用和配置，平台或其他数据透视表。
* **PackageReference 正处于积极开发**： 请参阅[在 GitHub 上发出 PackageReference](https://aka.ms/nuget-pr-improvements)。 packages.config 不再处于积极开发阶段。

### <a name="limitations"></a>限制

* NuGet PackageReference 不提供在 Visual Studio 2015 及更早版本。 只能在 Visual Studio 2017 中可以打开已迁移的项目。
* 迁移不是当前适用于 c + + 和 ASP.NET 项目。
* 某些包可能无法与 PackageReference 完全兼容。 有关详细信息，请参阅[包兼容性问题](#package-compatibility-issues)。

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
> 开始迁移之前，Visual Studio 创建项目的备份，可以通过[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。

1. 打开包含项目使用的解决方案`packages.config`。

1. 在中**解决方案资源管理器**，右键单击**引用**节点或`packages.config`文件，然后选择**将 packages.config 迁移到 PackageReference...**.

1. 迁移器会分析项目的 NuGet 包引用，并尝试对其进行分类**顶级依赖项**（直接安装的 NuGet 包） 和**可传递依赖项**（已作为顶级包的依赖项安装的包）。

   > [!Note]
   > PackageReference 支持可传递程序包还原，这意味着不必显式安装可传递依赖项动态地解析依赖项。

1. （可选）您可以选择将通过选择归类为作为顶级依赖项的可传递依赖项的 NuGet 包**顶级**包的选项。 此选项会自动设置包包含不间接流动的资产 (中的那些`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`文件夹)，这些标记为开发依赖项 (`developmentDependency = "true"`)。

1. 查看任何[包兼容性问题](#package-compatibility-issues)。

1. 选择**确定**可开始迁移。

1. 在迁移结束时，Visual Studio 所提供的备份、 已安装程序包 （顶级依赖项） 的列表，可传递依赖项，作为引用的包的列表和标识的开头的兼容性问题的列表的报表的路径迁移。 报表将保存到备份文件夹。

1. 验证解决方案生成并运行。 如果遇到问题，[在 GitHub 上提出问题](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回滚到 packages.config

1. 关闭已迁移的项目。

1. 将项目文件复制并`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 为项目文件夹。 如果它在项目根目录中存在，请删除 obj 文件夹。

1. 打开的项目。

1. 打开使用 Package Manager Console**工具 > NuGet 包管理器 > 程序包管理器控制台**菜单命令。

1. 在控制台中运行以下命令：

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>包兼容性问题

PackageReference 中不支持在 packages.config 中受支持的某些方面。 Migrator 分析，并检测此类问题。 按预期方式在迁移后，可能不会有一个或多个以下问题的任何包。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，将忽略"install.ps1"脚本

| | |
| --- | --- |
| **说明** | 利用 PackageReference，安装或卸载包时不执行 install.ps1 和 uninstall.ps1 PowerShell 脚本。 |
| **潜在影响** | 依赖于这些脚本以配置该目标项目中的某些行为的包可能无法按预期方式工作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，"内容"资产不可用

| | |
| --- | --- |
| **说明** | 在包中的资产`content`文件夹不支持使用 PackageReference，将被忽略。 PackageReference 添加了对支持`contentFiles`能够更好地可传递的支持和共享的内容。  |
| **潜在影响** | 中的资产`content`不会复制到项目和项目取决于是否存在这些资产的代码需要重构。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>在升级后安装包时，不会应用 XDT 转换

| | |
| --- | --- |
| **说明** | 利用 PackageReference 不支持 XDT 转换和`.xdt`安装或卸载包时，将忽略文件。   |
| **潜在影响** | XDT 转换不适用于任何项目的 XML 文件，最常`web.config.install.xdt`并`web.config.uninstall.xdt`，这意味着项目的` web.config`安装或卸载包时不更新文件。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，将忽略 lib 根中的程序集

| | |
| --- | --- |
| **说明** | 使用 PackageReference，程序集提供的根处`lib`文件夹，但没有目标框架特定子文件夹将被忽略。 NuGet 查找匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹，并将匹配的程序集安装到项目。 |
| **潜在影响** | 不具有匹配的目标框架名字对象 (TFM) 的项目的目标框架与对应的子文件夹的包可能不会像预期在转换后或故障迁移过程的安装 |

## <a name="found-an-issue-report-it"></a>发现了问题？ 报告它 ！

如果遇到问题的迁移体验，请[NuGet GitHub 存储库中提出问题](https://github.com/NuGet/Home/issues/)。
