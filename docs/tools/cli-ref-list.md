---
title: NuGet CLI 列表命令
description: Nuget.exe list 命令的引用
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549796"
---
# <a name="list-command-nuget-cli"></a>列出命令 (NuGet CLI)

**适用于：** 包使用、 发布&bullet;**支持的版本：** 所有

显示来自给定源的包列表。 如果指定了不到源，在全局配置文件中，定义所有源`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`，使用。 如果`NuGet.Config`不指定任何源，然后`list`使用默认的源 (nuget.org)。

## <a name="usage"></a>用法

```cli
nuget list [search terms] [options]
```

其中的可选搜索词将筛选显示的列表。 就像它们是在 nuget.org 上使用它们时，搜索词将应用于包、 标记和包说明的名称。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AllVersions | 列出所有版本的包。 默认情况下，显示仅最新的包版本。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| IncludeDelisted | *（3.2 +)* 显示取消列出的包。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 预发行版 | 在列表中包括预发行包。 |
| 源 | 指定要搜索的包源的列表。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
