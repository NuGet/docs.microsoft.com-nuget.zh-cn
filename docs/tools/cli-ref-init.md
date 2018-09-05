---
title: NuGet CLI init 命令
description: Nuget.exe init 命令参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551405"
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI)

**适用于：** 创建包&bullet;**支持的版本：** 3.3 +

将所有包从平面文件夹都复制到目标文件夹的所述，使用层次结构布局[将命令添加](cli-ref-add.md)。 即，使用`init`相当于使用`add`命令上每个包的文件夹中。

与使用`add`，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，例如 nuget.org 或专用服务器。

## <a name="usage"></a>用法

```cli
nuget init <source> <destination> [options]
```

其中`<source>`是包含包的文件夹和`<destination>`是本地文件夹或 UNC 路径名称将包复制到其中。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| Expand | 将所有文件都添加到包源，则添加每个包中与相同`-Expand`与`add`命令。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
