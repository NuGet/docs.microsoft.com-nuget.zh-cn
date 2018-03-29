---
title: NuGet CLI init 命令 |Microsoft 文档
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe init 命令参考
keywords: nuget init 引用，init 命令
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI)

**适用于：** ，创建包&bullet;**受支持的版本：** 3.3 +

将所有包从平面文件夹都复制到目标文件夹使用层次结构布局，按照所述的[将命令添加](cli-ref-add.md)。 即，使用`init`相当于使用`add`命令上每个包的文件夹中。

与`add`，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。

## <a name="usage"></a>用法

```cli
nuget init <source> <destination> [options]
```

其中`<source>`是包含包的文件夹和`<destination>`是本地文件夹或包复制到其中的 UNC 路径名。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定， `%AppData%\NuGet\NuGet.Config` (Windows) 或`~/.nuget/NuGet/NuGet.Config`使用 (Mac/Linux)。|
| ForceEnglishOutput | *（3.5 +)*强制 nuget.exe 运行使用固定的、 基于英语的区域性。 |
| Expand | 将所有文件都添加到包源，则添加每个包中与相同`-Expand`与`add`命令。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息量：*正常*， *quiet*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
