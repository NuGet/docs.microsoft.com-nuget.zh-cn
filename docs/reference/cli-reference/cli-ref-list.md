---
title: NuGet CLI 列表命令
description: 针对 nuget.exe list 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327734"
---
# <a name="list-command-nuget-cli"></a>list 命令 (NuGet CLI)

**适用于:** 包消耗, 发布&bullet; **支持的版本:** 全部

显示来自给定源的包的列表。 如果未指定任何源, 将使用全局配置文件`%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`中定义的所有源。 如果`NuGet.Config`未指定源, 则`list`使用默认源 (nuget.org)。

## <a name="usage"></a>用法

```cli
nuget list [search terms] [options]
```

其中, 可选搜索词将筛选显示的列表。 搜索词应用于包、标记和包说明的名称, 就像在 nuget.org 上使用时一样。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AllVersions | 列出包的所有版本。 默认情况下, 仅显示最新的包版本。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| IncludeDelisted | *(3.2 +)* 显示未列出的包。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 早期 | 在列表中包括预发行程序包。 |
| Source | 指定要搜索的包源列表。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
