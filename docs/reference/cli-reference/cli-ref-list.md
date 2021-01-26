---
title: NuGet CLI 列表命令
description: nuget.exe list 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 55ccf0d86ad6df8001e7401d430ec29cd7a154c3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780062"
---
# <a name="list-command-nuget-cli"></a> (NuGet CLI) 列表命令

**适用于：** 包消耗，发布 &bullet; **支持的版本：** 全部

显示来自给定源的包的列表。 如果未指定任何源，将使用全局配置文件中定义的所有源 `%AppData%\NuGet\NuGet.Config` (Windows) 或 `~/.nuget/NuGet/NuGet.Config` 。 如果 `NuGet.Config` 未指定源，则 `list` 使用默认源 (nuget.org) 。

## <a name="usage"></a>使用情况

```cli
nuget list [search terms] [options]
```

其中，可选搜索词将筛选显示的列表。 [搜索词](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 应用于包、标记和包说明的名称，就像在 nuget.org 上使用时一样。 

## <a name="options"></a>选项

- **`-AllVersions`**

  列出包的所有版本。 默认情况下，仅显示最新的包版本。

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-IncludeDelisted`**

  *(3.2 +)* 显示未列出的包。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-PreRelease`**

  在列表中包括预发行程序包。

- **`-Source`**

  要搜索的包源。 可以使用选项多次指定多个源 `-Source` 。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

列出配置的源中的所有包：
```
nuget list
```
列出与 Azure 相关的包，详细详细说明：
```
nuget list Azure -Verbosity detailed
```
列出来自配置的源的 Azure 相关包的所有版本：
```
nuget list Azure -AllVersions
```
列出指定源/源中与 JSON 相关的所有包的所有版本：
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
列出来自多个源/源的 JSON 相关包：
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
