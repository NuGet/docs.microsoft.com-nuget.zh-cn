---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327794"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 命令 (NuGet CLI)

**适用于:** 所有&bullet; **受支持的版本**: 全部

显示常规帮助信息和有关特定命令的帮助信息。

## <a name="usage"></a>用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中, [命令] 标识要显示其帮助的特定命令。

> [!Warning]
> 对于某些命令, 请注意首先指定*帮助*, `nuget help install`因为在 nuget.org 中有一个名为 "help" 的包。如果你指定了命令`nuget install help`, 则将不会获得有关安装命令的帮助, 但会改为安装名为 help 的程序包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 全部 | 打印所有可用命令的详细帮助;如果给定了特定命令, 则忽略。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示 help 命令本身的帮助信息。 |
| Markdown | 当与`-All`一起使用时, 打印 markdown 格式的详细帮助。 否则忽略。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
