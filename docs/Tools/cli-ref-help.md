---
title: "NuGet CLI help 命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe help 命令的引用"
keywords: "nuget 帮助参考，帮助命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>帮助或？ 命令 (NuGet CLI)

**适用于：**所有&bullet;**受支持的版本**： 所有

显示常规帮助信息和帮助有关特定命令的信息。

## <a name="usage"></a>用法

```
nuget help [command] [options]
nuget ? [command] [options]
```

其中 [命令] 标识要显示帮助其特定的命令。

> [!Warning]
> 使用某些命令，请注意指定*帮助*第一，作为家`nuget help install`，因为包 nuget.org 上名为"帮助"。如果你可以用以下命令`nuget install help`，你将安装命令获取帮助，但将改为安装名为帮助的程序包。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 全部 | 获取所有可用的命令; 帮助打印的详细的信息如果将给特定的命令被忽略。 |
| ConfigFile | *（2.5 +)* NuGet 要应用的配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助帮助命令本身的信息。 |
| Markdown | 打印 markdown 格式一起使用时的详细的帮助`-All`。 否则将忽略。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
