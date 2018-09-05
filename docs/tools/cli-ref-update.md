---
title: NuGet CLI update 命令
description: Nuget.exe 更新命令的引用
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc34550b3669d83466318645987cfd3078bc3c18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545095"
---
# <a name="update-command-nuget-cli"></a>update 命令 (NuGet CLI)

**适用于：** 打包消耗&bullet;**支持的版本：** 所有

更新项目中的所有包 (使用`packages.config`) 到其最新可用版本。 建议运行[还原](cli-ref-restore.md)运行之前`update`。 (若要更新的单个包，请使用[ `nuget install` ](cli-ref-install.md)而无需指定的版本号，在其中写 NuGet 安装最新版本。)

注意：`update`并不适用于 CLI 下运行 Mono （Mac OSX 或 Linux） 或使用 PackageReference 格式时。

`update`命令还会更新项目文件中的程序集引用、 提供这些引用已存在。 如果更新的包已添加的程序集，则新引用*不*添加。 新的包依赖项也没有添加其程序集引用。 若要更新的一部分中包括这些操作，更新 Visual Studio 中使用包管理器 UI 或程序包管理器控制台中的包。

此命令还可用于更新 nuget.exe 本身使用 *-自助*标志。

## <a name="usage"></a>用法

```cli
nuget update <configPath> [options]
```

其中`<configPath>`标识或者`packages.config`或解决方案文件，其中列出项目的依赖项。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| FileConflictAction | 指定当需要覆盖或忽略现有的项目所引用的文件时要执行的操作。 值为*覆盖，忽略无*。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| Id | 指定包 Id，以更新的列表。 |
| MSBuildPath | *（4.0 +)* 指定的路径优先于命令中使用 MSBuild `-MSBuildVersion`。 |
| MSBuildVersion | *（3.2 +)* 指定要用于此命令的 MSBuild 版本。 支持的值为 4、 12、 14、 15。 默认情况下，选择你的路径中的 MSBuild，否则它默认为最高的已安装版本的 MSBuild。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 预发行版 | 允许更新预发布版本。 更新已安装的预发行包时，则不需要此标志。 |
| RepositoryPath | 指定安装包的本地文件夹。 |
| 安全 | 指定仅更新使用相同的主版本号和次版本中可用的最高版本将安装已安装的程序包。 |
| 自助 | Nuget.exe 更新到最新版本;将忽略所有其他参数。 |
| 源 | 指定包源的列表 （作为 Url) 若要使用的更新。 如果省略，该命令使用在配置文件中提供的源，请参阅[配置 NuGet 行为](../consume-packages/configuring-nuget-behavior.md)。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |
| 版本 | 当用于一个包 ID，指定要更新的包的版本。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
