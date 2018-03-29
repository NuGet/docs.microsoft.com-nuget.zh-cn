---
title: NuGet CLI 还原命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 有关 nuget.exe 的还原命令的引用
keywords: nuget 还原引用，请还原包命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 64f12fdedc8fbfcee15c1dcddc445148f458c030
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="restore-command-nuget-cli"></a>restore 命令 (NuGet CLI)

**适用于：**打包消耗&bullet;**受支持的版本：** 2.7 +

下载并安装任何缺少的程序包`packages`文件夹。 如果用于 NuGet 4.0 + 和 PackageReference 格式，生成`<project>.nuget.props`文件，如果需要在`obj`文件夹。 （该文件可以省略从源代码管理。）

在 Mac OSX 和 Linux 上 Mono cli 上，还原程序包不支持 PackageReference。

## <a name="usage"></a>用法

```cli
nuget restore <projectPath> [options]
```

其中`<projectPath>`指定解决方案的位置或`packages.config`文件。 请参阅[备注](#remarks)下面有关行为的详细信息。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| DirectDownload | *（4.0 +)*直接而不填充缓存与任何二进制文件或元数据将下载包。 |
| DisableParallelProcessing | 禁用还原并行的多个包。 |
| FallbackSource | *（3.2 +)*要用作回退机制，以防主键中找不到包的包源的列表或默认源。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| MSBuildPath | *（4.0 +)*指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)*指定要用于此命令的 MSBuild 的版本。 支持的值为 4、 12、 14、 15。 默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。 |
| NoCache | 防止 NuGet 使用缓存的包。 请参阅[管理全局包和缓存文件夹](../consume-packages/managing-the-global-packages-and-cache-folders.md)。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| OutputDirectory | 指定在其中安装包的文件夹。 如果未不指定任何文件夹，则使用当前文件夹。 在使用进行还原时需要`packages.config`文件除非`PackagesDirectory`或`SolutionDirectory`使用。|
| PackageSaveMode | 指定要保存包安装完成后的文件类型： 之一`nuspec`， `nupkg`，或`nuspec;nupkg`。 |
| PackagesDirectory | 与 `OutputDirectory` 相同。 在使用进行还原时需要`packages.config`文件除非`OutputDirectory`或`SolutionDirectory`使用。 |
| Project2ProjectTimeOut | 超时 （秒） 来解析项目到项目引用。 |
| 递归 | *（4.0 +)*还原 UWP 和.NET 核心项目的所有引用项目。 不适用于使用项目`packages.config`。 |
| RequireConsent | 验证还原程序包启用了之前下载和安装包。 有关详细信息，请参阅[程序包还原](../consume-packages/package-restore.md)。 |
| SolutionDirectory | 指定的解决方案文件夹。 不还原解决方案的包时才有效。 在使用进行还原时需要`packages.config`文件除非`PackagesDirectory`或`OutputDirectory`使用。 |
| 源 | 指定包源的列表 （作为 Url) 要用于还原。 如果省略，则该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 |
| 详细级别 |> 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="remarks"></a>备注

还原命令执行以下步骤：

1. 确定还原命令的操作模式。
    projectPath 文件类型 | 行为
    | --- | --- |
    解决方案 （文件夹） | NuGet 中寻找`.sln`文件，然后使用，如果找到; 否则为会出错。 `(SolutionDir)\.nuget` 使用作为起始文件夹。
    `.sln` 文件 | 还原由解决方案; 标识的包如果将会出错`-SolutionDirectory`使用。 `$(SolutionDir)\.nuget` 使用作为起始文件夹。
    `packages.config` 或项目文件 | 还原文件，解决和安装依赖关系中列出的包。
    其他文件类型 | 文件被假定为`.sln`文件作为上述; 如果它不是一种解决方案，NuGet 提供的错误。
    (未指定 projectPath) | -NuGet 查找当前文件夹中的解决方案文件。 如果找到单个文件，一个用于还原包;如果找到多个解决方案，NuGet 将会出错。
    |-如果没有任何解决方案文件，查找 NuGet`packages.config`并使用该值来还原程序包。
    |-如果没有解决方案或`packages.config`文件找不到，NuGet 将会出错。

1. 确定使用以下优先级顺序 （如果没有这些文件夹发现，NuGet 都显示一条错误） 的包文件夹：

    - 使用指定的文件夹`-PackagesDirectory`。
    - `repositoryPath`中的值改 `Nuget.Config`
    - 使用指定的文件夹 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. 在还原时解决方案的包，NuGet 将执行以下操作：
    - 加载的解决方案文件。
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
