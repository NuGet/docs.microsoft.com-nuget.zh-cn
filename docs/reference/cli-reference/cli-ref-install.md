---
title: NuGet CLI 安装命令
description: 针对 nuget.exe install 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036937"
---
# <a name="install-command-nuget-cli"></a>install 命令 (NuGet CLI)

**适用于：** &bullet; 支持的**版本**的包使用：全部

使用指定的包源，将包下载并安装到项目中，默认为当前文件夹。

> [!Tip]
> 若要直接在项目上下文之外下载包，请访问[nuget.org](https://www.nuget.org)上的包页面，并选择 "**下载**" 链接。

如果未指定任何源，将使用全局配置文件中列出的 `%appdata%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。 有关更多详细信息，请参阅[常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。

如果未指定特定的包，`install` 将安装项目 `packages.config` 文件中列出的所有包，使其类似于[`restore`](cli-ref-restore.md)。

`install` 命令不会修改项目文件或 `packages.config`;通过这种方式，它与 `restore` 类似，只是将包添加到磁盘，但不会更改项目的依赖项。

若要添加依赖项，请在 Visual Studio 中通过包管理器 UI 或控制台添加包，或修改 `packages.config` 然后运行 `install` 或 `restore`。

## <a name="usage"></a>用法

```cli
nuget install <packageID | configFilePath> [options]
```

其中 `<packageID>` 命名要安装的包（使用最新版本），或 `<configFilePath>` 标识列出要安装的包的 `packages.config` 文件。 您可以使用 `-Version` 选项指示特定版本。

## <a name="options"></a>Options

| 选项 | 说明 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| DependencyVersion | *（4.4 +）* 要使用的依赖项包的版本，可以是下列项之一：<br/><ul><li>*最低*（默认值）：最低版本</li><li>*HighestPatch*：最小主要、次要和最高修补程序的版本</li><li>*HighestMinor*：最小主要版本号最高的版本，最高修补程序</li><li>*最高*：最高版本</li><li>*忽略*：将不使用任何依赖项包</li></ul> |
| DisableParallelProcessing | 禁止并行安装多个包。 |
| ExcludeVersion | 将包安装到仅带有包名称而不是版本号的名为的文件夹中。 |
| FallbackSource | *（3.2 +）* 在主或默认源中找不到包时要用作回退的包的列表。 |
| ForceEnglishOutput | *（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| 框架 | *（4.4 +）* 用于选择依赖项的目标框架。 如果未指定，默认值为 "Any"。 |
| 帮助 | 显示命令的帮助信息。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定在其中安装包的文件夹。 如果未指定文件夹，则使用当前文件夹。 |
| PackageSaveMode | 指定包安装后要保存的文件的类型： `nuspec`、`nupkg`或 `nuspec;nupkg`之一。 |
| PreRelease | 允许安装预发行程序包。 在 `packages.config`还原包时，不需要此标志。 |
| RequireConsent | 验证在下载和安装包之前是否启用了还原包。 有关详细信息，请参阅[包还原](../../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定要为其还原包的解决方案的根文件夹。 |
| 源 | 指定要使用的包源（作为 Url）的列表。 如果省略，则该命令使用配置文件中提供的源，请参阅[常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。 |
| 详细程度 | 指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。 |
| 版本 | 指定要安装的程序包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
