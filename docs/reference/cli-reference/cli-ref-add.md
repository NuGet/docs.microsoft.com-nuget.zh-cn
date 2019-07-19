---
title: NuGet CLI 添加命令
description: Nuget.exe add 命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327854"
---
# <a name="add-command-nuget-cli"></a>add 命令 (NuGet CLI)

**适用**于: 包发布&bullet; **支持的版本**:3.3+

将指定的包添加到分层布局中的非 HTTP 包源 (文件夹或 UNC 路径), 其中为包 ID 和版本号创建了文件夹。 例如:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

针对包源还原或更新时, 分层布局提供明显更好的性能。

若要将包中的所有文件展开到目标包源, 请使用`-Expand`开关。 这通常会导致在目标中出现其他子文件夹, 例如`tools`和`lib`。

## <a name="usage"></a>用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中`<packagePath>` , 是要添加的包的路径名, 并`<sourcePath>`指定要将包添加到的基于文件夹的包源。 HTTP 源不受支持。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定, `%AppData%\NuGet\NuGet.Config`则使用 (Windows `~/.nuget/NuGet/NuGet.Config` ) 或 (Mac/Linux)。|
| Expand | 将包中的所有文件添加到包源。 |
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
