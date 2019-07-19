---
title: NuGet CLI 局部变量命令
description: Nuget.exe 局部变量命令的参考
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327804"
---
# <a name="locals-command-nuget-cli"></a>locals 命令 (NuGet CLI)

**适用于:** 包&bullet;使用**受支持的版本:** 3.3+

清除或列出本地 NuGet 资源, 例如*http 缓存*、*全局包*文件夹和临时文件夹。 `locals`命令也可用于显示这些位置的列表。 有关详细信息, 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。

## <a name="usage"></a>用法

```cli
nuget locals <folder> [options]
```

其中`<folder>` `all`, 是`plugins-cache` 、 `global-packages` `temp`    、(3.5 及更早版本)、、(3.4 +) 和 (4.8 +) 之一。 `packages-cache` `http-cache`

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| 清除 | 清除指定的文件夹。 |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| 列表 | 列出指定文件夹的位置或所有文件夹在与*all*一起使用时的位置。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

有关其他示例, 请参阅[管理全局包和缓存文件夹](../../consume-packages/managing-the-global-packages-and-cache-folders.md)。
