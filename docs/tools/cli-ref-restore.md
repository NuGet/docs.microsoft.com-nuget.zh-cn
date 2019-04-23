---
title: NuGet CLI 还原命令
description: Nuget.exe restore 命令的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9964186dcbfedfbf2415a57102f8f019a1eef23a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931990"
---
# <a name="restore-command-nuget-cli"></a>restore 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**受支持的版本：** 2.7+

下载并安装缺少的任何包`packages`文件夹。 如果用于 NuGet 4.0 + 和 PackageReference 格式，将生成`<project>.nuget.props`文件，如果需要在`obj`文件夹。 （该文件可以省略从源代码管理。）

在 Mac OSX 和使用 Mono 上 CLI 在 Linux 上，还原包不支持使用 PackageReference。

## <a name="usage"></a>用法

```cli
nuget restore <projectPath> [options]
```

其中`<projectPath>`指定解决方案的位置或`packages.config`文件。 请参阅[备注](#remarks)下面有关行为的详细信息。

## <a name="options"></a>选项

| Option | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| DirectDownload | *（4.0 +)* 无填充任何二进制文件或元数据缓存，可直接下载包。 |
| DisableParallelProcessing | 禁用还原并行的多个包。 |
| FallbackSource | *（3.2 +)* 要用作回退，如果主数据库中找不到包的包源的列表或默认源。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| Help | 显示的帮助命令的信息。 |
| MSBuildPath | *（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要用于此命令的 MSBuild 版本。 支持的值为 4，12、 14、 15.1、 15.3、 15.4、 15.5、 15.6、 15.7、 15.8，15.9。 默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定在其中安装包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 使用还原时所需`packages.config`文件，除非`PackagesDirectory`或`SolutionDirectory`使用。|
| PackageSaveMode | 指定要将包安装完成后保存的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| PackagesDirectory | 与 `OutputDirectory` 相同。 使用还原时所需`packages.config`文件，除非`OutputDirectory`或`SolutionDirectory`使用。 |
| Project2ProjectTimeOut | 超时 （秒） 来解析项目到项目引用。 |
| 递归 | *（4.0 +)* 还原所有引用项目类型提供的 UWP 和.NET Core 项目。 不适用于使用项目`packages.config`。 |
| RequireConsent | 验证下载和安装包之前已启用还原包。 有关详细信息，请参阅[包还原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定的解决方案文件夹。 未还原解决方案的包时才有效。 使用还原时所需`packages.config`文件，除非`PackagesDirectory`或`OutputDirectory`使用。 |
| Source | 指定包源的列表 （作为 Url) 要用于还原。 如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 |
| Verbosity |> 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="remarks"></a>备注

Restore 命令将执行以下步骤：

1. 确定还原命令的操作模式。

   | projectPath 文件类型 | 行为 |
   | --- | --- |
   | 解决方案 （文件夹） | NuGet 将查找`.sln`文件，并使用，如果找到; 否则为会出错。 `(SolutionDir)\.nuget` 使用作为起始文件夹。 |
   | `.sln` 文件 | 还原由解决方案; 标识的包如果显示一条错误`-SolutionDirectory`使用。 `$(SolutionDir)\.nuget` 使用作为起始文件夹。 |
   | `packages.config` 或项目文件 | 还原文件，解决和安装依赖项中列出的包。 |
   | 其他文件类型 | 文件被假定为`.sln`文件作为更高版本; 如果它不是一种解决方案，NuGet 提供的错误。 |
   | (未指定 projectPath) | <ul><li>NuGet 将查找当前文件夹中的解决方案文件。 如果找到单个文件，一个用于还原的包;如果找到多个解决方案，NuGet 会出错。</li><li>如果没有任何解决方案文件，NuGet 将查找`packages.config`，并使用其还原包。</li><li>如果没有解决方案或`packages.config`找到文件，NuGet 会出错。</ul> |

2. 确定使用以下优先级顺序 （如果没有这些文件夹找到 NuGet 提供错误） 的包文件夹：

    - 使用指定的文件夹`-PackagesDirectory`。
    - `repositoryPath`中的值 `Nuget.Config`
    - 使用指定的文件夹 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 还原时解决方案的包，NuGet 将执行以下操作：
    - 加载解决方案文件。
    - 还原中列出的解决方案级别包`$(SolutionDir)\.nuget\packages.config`到`packages`文件夹。
    - 还原中列出的包`$(ProjectDir)\packages.config`到`packages`文件夹。 对于每个指定的包，还原并行中的包，除非`-DisableParallelProcessing`指定。

## <a name="examples"></a>示例

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
