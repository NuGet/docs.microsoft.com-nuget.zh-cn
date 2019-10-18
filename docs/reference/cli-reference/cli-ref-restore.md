---
title: NuGet CLI restore 命令
description: 针对 nuget.exe restore 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380461"
---
# <a name="restore-command-nuget-cli"></a>restore 命令（NuGet CLI）

**适用于：** 包消耗 &bullet;**支持的版本：** 2.7 +

下载并安装 `packages` 文件夹中缺少的任何程序包。 与 NuGet 4.0 + 和 PackageReference 格式一起使用时，会在 `obj` 文件夹中生成 `<project>.nuget.props` 文件（如果需要）。 （可以从源代码管理中省略该文件。）

在 Mono 上带有 CLI 的 Mac OSX 和 Linux 上，PackageReference 不支持还原包。

## <a name="usage"></a>用法

```cli
nuget restore <projectPath> [options]
```

其中 `<projectPath>` 指定解决方案或 `packages.config` 文件的位置。 有关行为的详细信息，请参阅下面的[备注](#remarks)。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| Read-configfile | 要应用的 NuGet 配置文件。 如果未指定，则使用 `%AppData%\NuGet\NuGet.Config` （Windows）或 `~/.nuget/NuGet/NuGet.Config` （Mac/Linux）。|
| DirectDownload | *（4.0 +）* 直接下载包，而不填充包含任何二进制文件或元数据的缓存。 |
| DisableParallelProcessing | 禁用并行还原多个包。 |
| FallbackSource | *（3.2 +）* 在主或默认源中找不到包时要用作回退的包的列表。 使用分号分隔列表项。 |
| ForceEnglishOutput | *（3.5 +）* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| 帮助 | 显示命令的帮助信息。 |
| MSBuildPath | *（4.0 +）* 指定要与命令一起使用的 MSBuild 的路径，其优先级高于 `-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +）* 指定要与此命令一起使用的 MSBuild 版本。 支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 默认情况下，将选取路径中的 MSBuild，否则默认为已安装的最高版本的 MSBuild。 |
| NoCache | 阻止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| 交互 | 禁止提示用户输入或确认。 |
| OutputDirectory | 指定在其中安装包的文件夹。 如果未指定文件夹，则使用当前文件夹。 当使用 `packages.config` 文件进行还原时必需，除非使用 `PackagesDirectory` 或 `SolutionDirectory`。|
| PackageSaveMode | 指定包安装后要保存的文件的类型： `nuspec`、`nupkg` 或 `nuspec;nupkg` 之一。 |
| PackagesDirectory | 与 `OutputDirectory` 相同。 当使用 `packages.config` 文件进行还原时必需，除非使用 `OutputDirectory` 或 `SolutionDirectory`。 |
| Project2ProjectTimeOut | 解析项目到项目引用的超时时间（秒）。 |
| recursive | *（4.0 +）* 还原 UWP 和 .NET Core 项目的所有引用项目。 不适用于使用 `packages.config` 的项目。 |
| RequireConsent | 验证在下载和安装包之前是否启用了还原包。 有关详细信息，请参阅[包还原](../../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定解决方案文件夹。 还原解决方案的包时无效。 当使用 `packages.config` 文件进行还原时必需，除非使用 `PackagesDirectory` 或 `OutputDirectory`。 |
| 源 | 指定要用于还原的包源（作为 Url）的列表。 如果省略，则该命令将使用配置文件中提供的源，请参阅[配置 NuGet 行为](../../consume-packages/configuring-nuget-behavior.md)。 使用分号分隔列表项。 |
| 团队 | 在基于 PackageReference 的项目中，将强制解析所有依赖项，即使上次还原已成功。 指定此标志与删除 `project.assets.json` 文件类似。 这不会绕过 http 缓存。 |
| 详细级别 | 指定在输出中显示的详细信息量： "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="remarks"></a>备注

Restore 命令执行以下步骤：

1. 确定 restore 命令的操作模式。

   | projectPath 文件类型 | 行为 |
   | --- | --- |
   | 解决方案（文件夹） | NuGet 查找 `.sln` 文件，如果找到，则使用该文件;否则，将产生错误。 `(SolutionDir)\.nuget` 用作起始文件夹。 |
   | `.sln` 文件 | 还原解决方案标识的包;如果使用 `-SolutionDirectory`，则会出现错误。 `$(SolutionDir)\.nuget` 用作起始文件夹。 |
   | `packages.config` 或项目文件 | 还原文件中列出的包，解析和安装依赖项。 |
   | 其他文件类型 | 文件被假定为上述 `.sln` 文件;如果它不是解决方案，NuGet 将会出现错误。 |
   | （未指定 projectPath） | <ul><li>NuGet 在当前文件夹中查找解决方案文件。 如果找到一个文件，则使用该文件还原包;如果找到多个解决方案，NuGet 将提供错误。</li><li>如果没有解决方案文件，NuGet 将查找 `packages.config`，并使用该文件还原包。</li><li>如果未找到任何解决方案或 `packages.config` 文件，NuGet 将提供错误。</ul> |

2. 使用以下优先级顺序确定包文件夹（如果找不到这些文件夹，则 NuGet 会出现错误）：

    - @No__t_0 指定的文件夹。
    - @No__t_1 中的 `repositoryPath` 值
    - 用 `-SolutionDirectory` 指定的文件夹
    - `$(SolutionDir)\packages`

3. 还原解决方案的包时，NuGet 会执行以下操作：
    - 加载解决方案文件。
    - 将 `$(SolutionDir)\.nuget\packages.config` 中列出的解决方案级别包还原到 `packages` 文件夹。
    - 将 `$(ProjectDir)\packages.config` 中列出的包还原到 `packages` 文件夹。 对于指定的每个包，请并行还原包，除非指定 `-DisableParallelProcessing`。

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
