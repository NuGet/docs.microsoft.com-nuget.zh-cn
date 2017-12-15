---
title: "NuGet CLI 列表命令 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "对于 nuget.exe 列出命令的引用"
keywords: "nuget 列表引用包列表的命令"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>(NuGet CLI) 中的列表命令

**适用于：**包消耗、 发布&bullet;**受支持的版本：**所有

显示从给定的源的包的列表。 如果未不指定任何源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`，使用。 如果`NuGet.Config`然后指定任何源`list`使用默认的源 (nuget.org)。

## <a name="usage"></a>用法

```
nuget list [search terms] [options]
```

其中可选的搜索词将筛选显示的列表。 搜索条款将应用到的包、 标记和包说明的名称。

## <a name="options"></a>选项
| 选项 | 描述 |
| --- | --- |
| AllVersions | 列出所有版本的包。 默认情况下，显示仅最新的包版本。 |
| ConfigFile | *（2.5 +)* NuGet 要应用的配置文件。 如果未指定， *%AppData%\NuGet\NuGet.Config*使用。 |
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| IncludeDelisted | *（3.2 +)*显示未列出的程序包。 |
| 非交互式 | 取消显示提示用户输入或确认。 |
| 预发行版 | 在列表中包含预发行程序包。 |
| 源 | 指定要搜索的程序包源的列表。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细 （2.5 +）*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
