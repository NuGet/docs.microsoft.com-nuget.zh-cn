---
title: NuGet CLI update 命令
description: 针对 nuget.exe update 命令的参考
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327504"
---
# <a name="update-command-nuget-cli"></a>update 命令 (NuGet CLI)

**适用于:** 包&bullet;使用**受支持的版本:** 全部

将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。 建议在运行`update`之前运行["还原"](cli-ref-restore.md) 。 (若要更新单个包, 请[`nuget install`](cli-ref-install.md)使用而不指定版本号, 在这种情况下, NuGet 安装最新版本。)

注意: `update`不适用于在 Mono (Mac OSX 或 Linux) 下运行的 CLI 或使用 PackageReference 格式。

`update`命令还会更新项目文件中的程序集引用, 前提是这些引用已存在。 如果更新的包具有添加的程序集, 则*不*会添加新引用。 新的包依赖项也没有添加其程序集引用。 若要将这些操作包括为更新的一部分, 请使用包管理器 UI 或程序包管理器控制台在 Visual Studio 中更新包。

此命令还可用于使用 *-self*标志更新 nuget.exe 本身。

## <a name="usage"></a>用法

```cli
nuget update <configPath> [options]
```

其中`<configPath>` 标识`packages.config`列出项目依赖项的或解决方案文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| FileConflictAction | 指定在要求覆盖或忽略项目引用的现有文件时要执行的操作。 值为*overwrite、ignore、none*。 |
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| Id | 指定要更新的包 Id 列表。 |
| MSBuildPath | *(4.0 +)* 指定要与命令一起使用的 MSBuild 的路径, 优先于`-MSBuildVersion`。 |
| MSBuildVersion | *(3.2 +)* 指定要与此命令一起使用的 MSBuild 版本。 支持的值为4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 默认情况下, 将选取路径中的 MSBuild, 否则默认为已安装的最高版本的 MSBuild。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 早期 | 允许更新到预发布版本。 更新已安装的预发布包时, 不需要此标志。 |
| RepositoryPath | 指定安装包的本地文件夹。 |
| 防 | 指定仅安装具有与安装包相同的主要版本和次要版本中可用的最高版本的更新。 |
| 解压 | 将 nuget.exe 更新到最新版本;忽略所有其他参数。 |
| Source | 指定要用于更新的包源 (作为 Url) 的列表。 如果省略, 则该命令使用配置文件中提供的源, 请参阅[常见的 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |
| Version | 与一个包 ID 一起使用时, 指定要更新的包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
