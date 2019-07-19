---
title: NuGet 更新-包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的更新包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327264"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package （Visual Studio 中的程序包管理器控制台）

*仅在 Windows 上的 Visual Studio 中的[NuGet 包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内可用。*

将包及其依赖项或项目中的所有包更新到较新的版本。

## <a name="syntax"></a>语法

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中`Update-Package` , 可以使用来降级项目中的现有包。 例如, 如果安装了 5.1.0-rc1, 以下命令会将其降级到 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>参数

|  参数 | 描述 |
| --- | --- |
| Id | 要更新的包的标识符。 如果省略, 则更新所有包。 -Id 开关本身是可选的。 |
| IgnoreDependencies | 跳过更新包的依赖项。 |
| ProjectName | 包含要更新的包的项目的名称, 默认为 "所有项目"。 |
| Version | 要用于升级的版本, 默认为最新版本。 在 NuGet 3.0 + 中, 版本值必须为*最低、最高、HighestMinor*或*HighestPatch* (等效于-安全) 之一。 |
| 防 | 仅将升级限制为与当前安装的包具有相同的主版本和次版本的版本。 |
| Source | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径, 也可以是相对于当前文件夹的路径。 如果省略, `Update-Package`则搜索当前选定的包源。 |
| IncludePrerelease | 包含更新的预发布包。 |
| 重新安装 | 使用当前安装的版本 Resintalls 包。 请参阅[重新安装和更新包](../../consume-packages/reinstalling-and-updating-packages.md)。 |
| FileConflictAction | 当要求覆盖或忽略项目引用的现有文件时要执行的操作。 可能的值包括*Overwrite、Ignore、None、OverwriteAll*和*IgnoreAll* (3.0 +)。 |
| DependencyVersion | 要使用的依赖项包的版本, 可以是下列项之一:<br/><ul><li>*最低*(默认值): 最低版本</li><li>*HighestPatch*: 最小主要、次要和最高修补程序的版本</li><li>*HighestMinor*: 最小主要版本号最高的版本, 最高修补程序</li><li>*最高*(不带参数的更新包的默认值): 最高版本</li></ul>您可以使用[`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config`文件中的设置设置默认值。 |
| ToHighestPatch | 等效于-Safe。 |
| ToHighestMinor | 仅将升级限制为版本与当前安装的包相同的版本。 |
| WhatIf | 显示运行命令时, 不实际执行更新的情况。 |

这些参数都不接受管道输入或通配符。

### <a name="common-parameters"></a>通用参数

`Update-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

### <a name="examples"></a>示例

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
