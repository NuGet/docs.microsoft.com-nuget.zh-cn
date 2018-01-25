---
title: "NuGet CLI 更新命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 更新命令参考"
keywords: "nuget 更新引用，更新包命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 891ce1f27102b16125c93e7a66ebd29f6fc626db
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="update-command-nuget-cli"></a>(NuGet CLI) 中的更新命令

**适用于：**打包消耗&bullet;**受支持的版本：**所有

更新的项目中的所有包 (使用`packages.config`) 到其最新的可用版本。 建议运行[还原](cli-ref-restore.md)之前运行`update`。 (若要更新的单个包，使用[ `nuget install` ](cli-ref-install.md)而无需指定的版本号，在其中事例 NuGet 安装最新版本。)

注意：`update`并不适用于运行下 Mono （Mac OSX 或 Linux） 或使用 PackageReference 格式时的 CLI。

`update`命令还会更新项目文件中的程序集引用、 提供这些引用已存在。 如果更新后的包已添加的程序集，新的引用的是*不*添加。 新的包依赖关系还没有添加其程序集引用。 若要更新的一部分中包括这些操作，更新使用程序包管理器 UI 或包管理器控制台的 Visual Studio 中的包。

此命令还可以用于更新 nuget.exe 本身使用*-自助*标志。

## <a name="usage"></a>用法

```cli
nuget update <configPath> [options]
```

其中`<configPath>`标识是`packages.config`或列出了项目的依赖关系的解决方案文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| FileConflictAction | 指定当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行的操作。 值为*覆盖，请忽略，无*。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| Id | 指定的包 Id，以更新的列表。 |
| MSBuildPath | *（4.0 +)*指定 MSBuild 使用执行命令，优先于的路径`-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)*指定要用于此命令的 MSBuild 的版本。 支持的值为 4、 12、 14、 15。 默认情况下，选择你的路径中的 MSBuild，否则，它默认为最高的已安装版本的 MSBuild。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 预发行版 | 允许更新到的预发布版本。 如果更新已安装的预发行包，则不需要此标志。 |
| RepositoryPath | 指定包的安装位置的本地文件夹。 |
| 安全 | 指定仅更新在相同的主版本号和次版本中可用的最高版本的已安装的程序包将安装。 |
| 自助 | 更新 nuget.exe 的最新版本;将忽略所有其他参数。 |
| 源 | 指定包源的列表 （作为 Url) 若要使用的更新。 如果省略，则该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../Consume-Packages/Configuring-NuGet-Behavior.md)。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |
| 版本 | 当与一个包 ID 一起使用，指定要更新的包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
