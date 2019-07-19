---
title: NuGet CLI 初始化命令
description: Nuget.exe init 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327774"
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI)

**适用于:** 创建&bullet;包的**支持版本:** 3.3+

使用 "[添加" 命令](cli-ref-add.md)所述的分层布局, 将平面文件夹中的所有包复制到目标文件夹。 也就是说, 使用`init`等效于对文件夹中的`add`每个包使用命令。

对于`add`, 目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库, 如 nuget.org 或专用服务器。

## <a name="usage"></a>用法

```cli
nuget init <source> <destination> [options]
```

其中`<source>` , 是包含包的文件夹`<destination>` , 是要将包复制到的本地文件夹或 UNC 路径名。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Expand | 添加添加到包源的每个包中的所有文件;`-Expand` 与`add`命令相同。 |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
