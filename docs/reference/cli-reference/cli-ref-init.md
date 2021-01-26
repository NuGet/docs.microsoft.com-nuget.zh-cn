---
title: NuGet CLI 初始化命令
description: nuget.exe init 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780064"
---
# <a name="init-command-nuget-cli"></a>init 命令 (NuGet CLI) 

**适用于：** 创建包的 &bullet; **支持版本：** 3.3 +

使用 " [添加" 命令](cli-ref-add.md)所述的分层布局，将平面文件夹中的所有包复制到目标文件夹。 也就是说，使用 `init` 等效于对 `add` 文件夹中的每个包使用命令。

对于 `add` ，目标必须是本地文件夹或 UNC 路径;不支持 HTTP 包存储库，如 nuget.org 或专用服务器。

## <a name="usage"></a>使用情况

```cli
nuget init <source> <destination> [options]
```

其中 `<source>` ，是包含包的文件夹， `<destination>` 是要将包复制到的本地文件夹或 UNC 路径名。

## <a name="options"></a>选项

- **`-ConfigFile`**

  要应用的 NuGet 配置文件。 如果未指定，则 `%AppData%\NuGet\NuGet.Config` 使用 (Windows) `~/.nuget/NuGet/NuGet.Config` 或 `~/.config/NuGet/NuGet.Config` (Mac/Linux) 。

- **`-Expand`**

  添加添加到包源的每个包中的所有文件;与 `-Expand` `add` 命令相同。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 使用固定的、基于英语的区域性强制运行 nuget.exe。

- **`-?|-help`**

  显示命令的帮助信息。

- **`-NonInteractive`**

  禁止提示用户输入或确认。

- **`-Verbosity [normal|quiet|detailed]`**

  指定在输出中显示的详细信息的数量： `normal` (默认) 、 `quiet` 或 `detailed` 。

另请参阅 [环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
