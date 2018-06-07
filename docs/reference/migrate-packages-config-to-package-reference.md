---
title: 从 package.config 迁移到 PackageReference 格式
description: 有关如何将从 package.config 管理格式的项目迁移到 PackageReference NuGet 4.0 + 和 VS2017 和.NET 核心 2.0 所支持的详细信息
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: e0a4363a2807874ec8e2693c5b1c1a0eb2e8af0e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818781"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a>将从 packages.config 迁移到 PackageReference

Visual Studio 2017 版本 15.7年预览版 3年和更高版本中迁移从项目的支持[packages.config](./packages-config.md)管理格式[PackageReference](../consume-packages/Package-References-in-Project-Files.md)格式。

## <a name="benefits-of-using-packagereference"></a>使用 PackageReference 的好处

* **管理在一个位置的所有项目依赖项**： 一样项目到项目引用和程序集引用，NuGet 包引用 (使用`PackageReference`节点) 直接在项目文件中管理，而不是使用单独packages.config 文件。
* **顶级依赖项的整洁的视图**： 与 packages.config，不同 PackageReference 列出这些项目中直接安装的 NuGet 包。 因此，NuGet 包管理器 UI 和项目文件不杂乱具有低级别依赖项。
* **性能改进**： 如果使用 PackageReference，包将保留在*全局包*文件夹 (如所述[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)而不是在`packages`解决方案中的文件夹。 因此，PackageReference 执行得更快，并使用较少的磁盘空间。
* **微调对依赖关系和内容的流控制**： 使用 MSBuild 的现有功能允许你为[有条件地引用 NuGet 包](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)选择每个目标框架的包引用和配置，平台或其他透视。
* **PackageReference 是进行活动开发**： 请参阅[PackageReference 发出在 GitHub 上](https://aka.ms/nuget-pr-improvements)。 packages.config 不再进行活动开发。

### <a name="limitations"></a>限制

* NuGet PackageReference 不位于 Visual Studio 2015 及更早版本。 只能在 Visual Studio 2017 中，可以打开迁移的项目。
* 迁移不是当前可用于 c + + 和 ASP.NET 项目。
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
> 开始迁移之前，Visual Studio 将创建该项目的备份以使您能够[回滚到 packages.config](#how-to-roll-back-to-packagesconfig)如有必要。

1. 打开包含项目使用的解决方案`packages.config`。

1. 在**解决方案资源管理器**，右键单击**引用**节点或`packages.config`文件，然后选择**将 packages.config 迁移到 PackageReference...**.

1. 迁移器分析项目的 NuGet 包引用，并尝试对其进行分类入**顶级依赖项**（NuGet 包你安装目录） 和**可传递的依赖关系**（顶级包的依赖关系中已安装的包）。

   > [!Note]
   > PackageReference 支持可传递的程序包还原并解析依赖项动态，这意味着需要显式安装可传递的依赖关系。

1. （可选）你可以选择将通过选择归类为传递的依赖关系作为顶级依赖项 NuGet 包**顶级**包的选项。 包含不间接流的资产的包将自动设置此选项 (中的那些`build`， `buildCrossTargeting`， `contentFiles`，或`analyzers`文件夹)，这些标记为开发依赖项 (`developmentDependency = "true"`)。

1. 查看任何[包兼容性问题](#package-compatibility-issues)。

1. 选择**确定**可开始迁移。

1. 在迁移结束时，Visual Studio 具有路径的报表提供备份、 安装程序包 （顶级依赖项） 的列表，可传递的依赖关系引用的包的列表和列表的开头所述的兼容性问题迁移。 报表保存到备份文件夹。

1. 验证解决方案将生成并运行。 如果你遇到问题， [GitHub 上的文件出现问题](https://github.com/NuGet/Home/issues/)。

## <a name="how-to-roll-back-to-packagesconfig"></a>如何回滚到 packages.config

1. 关闭已迁移的项目。

1. 将项目文件复制和`packages.config`从备份 (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 到项目文件夹。 如果它存在于项目根目录 obj 文件夹，请将其删除。

1. 打开项目。

1. 打开程序包管理器控制台使用**工具 > NuGet 包管理器 > 程序包管理器控制台**菜单命令。

1. 在控制台中运行以下命令：

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a>包兼容性问题

PackageReference 中不支持在 packages.config 中受支持的某些方面。 迁移器分析，并检测到此类问题。 按预期在迁移后，可能无法正常工作的任何包都具有一个或多个以下的问题。

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，将忽略"install.ps1"脚本

| | |
| --- | --- |
| **说明** | 与 PackageReference，install.ps1，uninstall.ps1 PowerShell 脚本将不安装或卸载程序包时执行。 |
| **潜在影响** | 包依赖于这些脚本以配置目标项目中的某些行为可能不会按预期工作。 |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，"内容"资产不可用

| | |
| --- | --- |
| **说明** | 包中的资产`content`文件夹不支持 PackageReference 和将被忽略。 PackageReference 增加了对支持`contentFiles`能够更好地可传递的支持和共享的内容。  |
| **潜在影响** | 中的资产`content`不会复制到项目和项目取决于这些资产是否存在的代码需要重构。  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a>升级之后安装此包时，不会应用 XDT 转换

| | |
| --- | --- |
| **说明** | XDT 转换不支持 PackageReference 和`.xdt`安装或卸载程序包时忽略文件。   |
| **潜在影响** | XDT 转换不会应用与任何项目的 XML 文件，通常情况下，`web.config.install.xdt`和`web.config.uninstall.xdt`，这意味着项目的` web.config`安装或卸载该包时，不会更新文件。 |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a>在迁移后安装此包时，将忽略 lib 根中的程序集

| | |
| --- | --- |
| **说明** | PackageReference，与程序集存在根目录下的`lib`而无需的目标 framework 的特定子文件夹的文件夹将被忽略。 NuGet 查找匹配的目标框架名字对象 (TFM) 的项目的目标框架所对应的子文件夹，并在项目中安装匹配的程序集。 |
| **潜在影响** | 没有匹配的目标框架名字对象 (TFM) 的项目的目标框架所对应的子文件夹的包可能不会像预期的那样在转换后或失败迁移期间的安装 |

## <a name="found-an-issue-report-it"></a>发现了一个问题？ 报告它 ！

如果你遇到迁移体验问题，请[NuGet GitHub 存储库上的文件出现问题](https://github.com/NuGet/Home/issues/)。
