---
title: NuGet 同步-包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的同步包 PowerShell 命令引用。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384898"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package （Visual Studio 中的程序包管理器控制台）

*版本 3.0 +;仅在 Windows 上的 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*

从指定的（或默认的）项目获取已安装包的版本，并将该版本同步到解决方案中项目的其余部分。

## <a name="syntax"></a>语法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | 请求要同步的包的标识符。-Id 开关本身是可选的。 |
| IgnoreDependencies | 仅安装此程序包，而不安装其依赖项。 |
| ProjectName | 要从中同步包的项目，默认为默认项目。 |
| {2&gt;版本&lt;2} | 要同步的包版本，默认为当前安装的版本。 |
| Source | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。 如果省略，则 `Sync-Package` 搜索当前选定的包源。 |
| IncludePrerelease | 包括同步中的预发行包。 |
| FileConflictAction | 当要求覆盖或忽略项目引用的现有文件时要执行的操作。 可能的值包括*Overwrite、Ignore、None、OverwriteAll*和 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 要使用的依赖项包的版本，可以是下列项之一：<br/><ul><li>*最低*（默认值）：最低版本</li><li>*HighestPatch*：最小主要、次要和最高修补程序的版本</li><li>*HighestMinor*：最小主要版本号最高的版本，最高修补程序</li><li>*最高*（不带参数的更新包的默认值）：最高版本</li></ul>您可以使用 `Nuget.Config` 文件中的[`dependencyVersion`](../nuget-config-file.md#config-section)设置设置默认值。 |
| WhatIf | 显示运行命令时，不实际执行同步的情况。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Sync-Package` 支持以下[常见的 PowerShell 参数](https://go.microsoft.com/fwlink/?LinkID=113216)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
