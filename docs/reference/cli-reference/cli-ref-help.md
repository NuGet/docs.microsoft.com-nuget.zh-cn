---
title: NuGet CLI 帮助命令
description: nuget.exe help 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779357"
---
# <a name="help-or--command-nuget-cli"></a>help or ?  (NuGet CLI) 的命令

**适用于：** 所有 &bullet; **受支持的版本**：全部

显示常规帮助信息和有关特定命令的帮助信息。

## <a name="usage"></a>使用情况

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中，[命令] 标识要显示其帮助的特定命令。

> [!Warning]
> 对于某些命令，请注意首先指定 *帮助* ， `nuget help install` 因为在 nuget.org 中有一个名为 "help" 的包。如果你指定了命令 `nuget install help` ，则将不会获得有关安装命令的帮助，但会改为安装名为 help 的程序包。

## <a name="options"></a>选项

- **`-All`**

  打印所有可用命令的详细帮助;如果给定了特定命令，则忽略。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-Markdown`**

  当与一起使用时，打印 markdown 格式的详细帮助 `-All` 。 否则忽略。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
