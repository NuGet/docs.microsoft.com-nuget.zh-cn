---
title: NuGet CLI 规范命令
description: nuget.exe spec 命令的参考
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779141"
---
# <a name="spec-command-nuget-cli"></a> (NuGet CLI 的 spec 命令) 

**适用于：** 创建包的 &bullet; **支持版本：** 全部

`.nuspec`为新包生成文件。 如果在与项目文件相同的文件夹中运行 (`.csproj` ， `.vbproj` `.fsproj`) `spec` 创建一个标记化 `.nuspec` 文件。 有关其他信息，请参阅 [创建包](../../create-packages/creating-a-package.md)。

## <a name="usage"></a>使用情况

```cli
nuget spec [<packageID>] [options]
```

其中 `<packageID>` 是要保存到文件中的可选包标识符 `.nuspec` 。

## <a name="options"></a>选项

- **`-AssemblyPath`**

  指定要用于元数据的程序集的路径。

- **`-Force`**

  覆盖任何现有 `.nuspec` 文件。


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
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
