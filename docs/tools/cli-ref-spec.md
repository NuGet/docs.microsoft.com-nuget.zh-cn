---
title: NuGet CLI spec 命令
description: Nuget.exe spec 命令参考
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794146"
---
# <a name="spec-command-nuget-cli"></a>spec 命令 (NuGet CLI)

**适用于：** 创建包&bullet;**支持的版本：** 所有

生成`.nuspec`新包文件。 如果在项目文件所在的文件夹中运行 (`.csproj`， `.vbproj`， `.fsproj`)，`spec`创建已标记化`.nuspec`文件。 有关其他信息，请参阅[创建包](../create-packages/creating-a-package.md)。

## <a name="usage"></a>用法

```cli
nuget spec [<packageID>] [options]
```

其中`<packageID>`是一个可选包标识符，以将保存在`.nuspec`文件。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AssemblyPath | 指定要用于元数据的程序集的路径。 |
| 强制 | 将覆盖任何现有`.nuspec`文件。 |
| ForceEnglishOutput | *（3.5 +)* 强制 nuget.exe 以运行使用固定的、 基于英语的区域性。 |
| 帮助 | 显示的帮助命令的信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| 详细级别 | 指定的输出中显示的详细信息：*正常*，*静默*，*详细*。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
