---
title: NuGet CLI 添加命令
description: Nuget.exe 的引用添加命令
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545829"
---
# <a name="add-command-nuget-cli"></a>add 命令 (NuGet CLI)

**适用于**： 包发布&bullet;**支持的版本**: 3.3 +

将指定的包添加到层次结构的布局，其中包 ID 和版本编号创建的文件夹中的非 HTTP 包源 （文件夹或 UNC 路径）。 例如：

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

还原或更新时对包源，层次结构布局提供了显著提高性能。

若要扩展到的目标包源的包中的所有文件，使用`-Expand`切换。 这通常会出现在该目标，如其他子文件夹中`tools`和`lib`。

## <a name="usage"></a>用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

其中`<packagePath>`是要添加的包的路径名和`<sourcePath>`指定可向其添加包的基于文件夹的包源。 不支持 HTTP 源。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| ConfigFile | 要应用的 NuGet 配置文件。 如果未指定，否则`%AppData%\NuGet\NuGet.Config`(Windows) 或`~/.nuget/NuGet/NuGet.Config`(Mac/Linux) 使用。|
| Expand | 将包中的所有文件都添加到包源。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| Help | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
