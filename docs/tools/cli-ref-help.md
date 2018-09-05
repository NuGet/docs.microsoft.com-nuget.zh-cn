---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546558"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 命令 (NuGet CLI)

**适用于：** 所有&bullet;**支持的版本**： 所有

显示常规技术信息和帮助有关特定命令的信息。

## <a name="usage"></a>用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [command]，标识要为其显示帮助特定的命令。

> [!Warning]
> 某些命令，请注意以指定*帮助*首先，作为与`nuget help install`，因为名为 nuget.org 上的"帮助"的包。如果你向命令提供`nuget install help`，你不会在安装命令上获取帮助，但将改为安装名为帮助的包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 全部 | 获取所有可用的命令; 帮助打印的详细的信息提供特定的命令将被忽略。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示帮助信息用于帮助命令本身。 |
| Markdown | 打印 markdown 格式与一起使用时的详细的帮助`-All`。 否则将忽略。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
