---
title: NuGet CLI 帮助命令
description: Nuget.exe help 命令的引用
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818251"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 命令 (NuGet CLI)

**适用于：** 所有&bullet;**受支持的版本**： 所有

显示常规帮助信息和帮助有关特定命令的信息。

## <a name="usage"></a>用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [命令] 标识要显示帮助其特定的命令。

> [!Warning]
> 使用某些命令，请注意指定*帮助*第一，作为家`nuget help install`，因为包 nuget.org 上名为"帮助"。如果你可以用以下命令`nuget install help`，不会获取有关安装命令的帮助，但将改为安装名为帮助的程序包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 全部 | 获取所有可用的命令; 帮助打印的详细的信息如果将给特定的命令被忽略。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助帮助命令本身的信息。 |
| Markdown | 打印 markdown 格式一起使用时的详细的帮助`-All`。 否则将忽略。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
