---
title: NuGet CLI 规范命令
description: Nuget.exe 规范命令的参考
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327564"
---
# <a name="spec-command-nuget-cli"></a>spec 命令 (NuGet CLI)

**适用于:** 创建&bullet;包的**支持版本:** 全部

为新包生成文件。`.nuspec` 如果在与项目文件相同的文件夹中运行 (`.csproj`、 `.vbproj`、 `.fsproj`), `spec`则将创建`.nuspec`一个标记化文件。 有关其他信息, 请参阅[创建包](../../create-packages/creating-a-package.md)。

## <a name="usage"></a>用法

```cli
nuget spec [<packageID>] [options]
```

其中`<packageID>`是要保存到`.nuspec`文件中的可选包标识符。

## <a name="options"></a>选项

| 选项 | 描述 |
| --- | --- |
| AssemblyPath | 指定要用于元数据的程序集的路径。 |
| 团队 | 覆盖任何现有`.nuspec`文件。 |
| ForceEnglishOutput | *(3.5 +)* 使用固定的、基于英语的区域性强制执行 nuget.exe。 |
| Help | 显示命令的帮助信息。 |
| NonInteractive | 取消显示提示用户输入或确认。 |
| Verbosity | 指定在输出中显示的详细信息量: "*正常*"、"*静默*"、"*详细*"。 |

另请参阅[环境变量](cli-ref-environment-variables.md)

## <a name="examples"></a>示例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
