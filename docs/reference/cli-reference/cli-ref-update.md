---
title: NuGet CLI 更新命令
description: nuget.exe update 命令的引用
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323643"
---
# <a name="update-command-nuget-cli"></a>NuGet CLI (update) 

**适用于：包** 消耗 &bullet; **支持的版本：** 全部

将项目中的所有包（使用 `packages.config`）更新为其最新可用版本。 建议在运行 [之前运行"还原](cli-ref-restore.md) `update` "。  (若要更新单个包，请使用 而不指定版本号，在这种情况下 [`nuget install`](cli-ref-install.md) ，NuGet 将安装最新版本.) 

注意：在 Mono 下运行的 CLI (Mac OSX 或 Linux) `update` 使用 PackageReference 格式时。

该命令 `update` 还会更新项目文件中程序集引用，只要这些引用已存在。 如果更新的包具有已添加的程序集，则不添加 *新* 引用。 新包依赖项也尚未添加其程序集引用。 若要在更新中包括这些操作，请通过 Visual Studio UI 或 程序包管理器 控制台程序包管理器包。

此命令还可用于使用 -self nuget.exe自行 *更新。*

## <a name="usage"></a>使用情况

```cli
nuget update <configPath> [options]
```

其中 `<configPath>` 标识列出 `packages.config` 项目依赖项的 或 解决方案文件。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 (Windows) 或 `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` (`~/.config/NuGet/NuGet.Config` Mac/Linux) 。
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  指定要使用的依赖项包的版本，可以是以下项之一：<br/><ul><li>*最低* (默认) ：最低版本</li><li>*HighestPatch：* 主要版本最低、次要版本最低、修补程序最高版本</li><li>*HighestMinor：* 具有最低主要版本、最高次要版本、最高修补程序版本</li><li>*最高*：最高版本</li><li>*忽略*：不会使用依赖项包</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  指定目标项目中已存在包中的文件时的默认操作。 将 设置为 `Overwrite` 以始终覆盖文件。 设置为 可 `Ignore` 跳过文件。

  除非提供 或 ，否则操作（默认）将提示输入每个冲突文件，这将 `PromptUser` `OverwriteAll` `IgnoreAll` 应用于所有剩余文件。

- **`-ForceEnglishOutput`**

  *(3.5+)* 强制nuget.exe使用固定、基于英语的区域性运行。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-Id`**

  指定要更新的包 ID 的列表。

- **`-MSBuildPath`**

  *(4.0+)* 指定要与 命令一起使用的 MSBuild 路径，并优先于 `-MSBuildVersion` 。

- **`-MSBuildVersion`**

  *(3.2+)* 指定要与此命令一起使用的 MSBuild 版本。 支持的值包括 4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9。 默认情况下，选择路径中的 MSBuild，否则默认为最高安装的 MSBuild 版本。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-PreRelease`**

  允许更新到预发行版本。 更新已安装的预发行包时，不需要此标志。

- **`-RepositoryPath`**

  指定安装包的本地文件夹。

- **`-Safe`**

  指定只会安装与已安装包相同的主版本和次要版本中可用的最高版本的更新。

- **`-Self`**

  对 `nuget.exe` 最新版本的更新。 `-Source` 可以使用 ，但忽略所有其他参数。 如果未提供源，则 `nuget.org` 检查更新，而不考虑 `NuGet.Config` 设置。

- **`-Source`**

  指定要用作更新 (URL) 包源的列表。 如果省略，该命令将使用配置文件中提供的源，请参阅 [常见 NuGet 配置](../../consume-packages/configuring-nuget-behavior.md)。

- **`-Verbosity [normal|quiet|detailed]`**

  指定输出中显示的详细信息量： (`normal` 默认 `quiet`) 、 或 `detailed` 。

- **`-Version`**

  与一个包 ID 一同使用时， 指定要更新的包的版本。

另 [请参阅环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
