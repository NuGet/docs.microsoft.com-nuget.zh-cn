---
title: NuGet Sync-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Sync-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238044"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Sync-Package (程序包管理器控制台) 

*版本 3.0 +;仅在 Windows 上的 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内可用。*

从指定 (或默认) 项目中获取已安装包的版本，并将该版本同步到解决方案中项目的其余部分。

## <a name="syntax"></a>语法

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>parameters

| 参数 | 说明 |
| --- | --- |
| ID | 需要 () 要同步的包的标识符。-Id 开关本身是可选的。 |
| IgnoreDependencies | 仅安装此程序包，而不安装其依赖项。 |
| 项目名称 | 要从中同步包的项目，默认为默认项目。 |
| 版本 | 要同步的包版本，默认为当前安装的版本。 |
| 源 | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。 如果省略，则 `Sync-Package` 搜索当前选定的包源。 |
| IncludePrerelease | 包括同步中的预发行包。 |
| FileConflictAction | 当要求覆盖或忽略项目引用的现有文件时要执行的操作。 可能的值包括 *Overwrite、Ignore、None、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。 |
| DependencyVersion | 要使用的依赖项包的版本，可以是下列项之一：<br/><ul><li>*最低* (默认) ：最低版本</li><li>*HighestPatch* ：最小主要、次要和最高修补程序的版本</li><li>*HighestMinor* ：最小主要版本号最高的版本，最高修补程序</li><li>不带参数的 Update-Package 的 *最高* (默认值) ：最高版本</li></ul>您可以使用文件中的设置设置默认值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。 |
| WhatIf | 显示运行命令时，不实际执行同步的情况。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Sync-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

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