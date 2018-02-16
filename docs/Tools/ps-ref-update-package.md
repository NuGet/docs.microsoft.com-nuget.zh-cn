---
title: "NuGet 更新包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "在 Visual Studio 中的 NuGet 包管理器控制台中的更新包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，更新包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ebb5a420e469c70a9dd790231a92fedbc4713b6
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>更新包 （在 Visual Studio 中的包管理器控制台）

*仅在内可用[NuGet 程序包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。*

更新到较新版本的包和其依赖项或在项目中，所有包。

## <a name="syntax"></a>语法

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 +`Update-Package`可用来将你的项目中的现有包降级。 例如，如果你有 Microsoft.AspNet.MVC 5.1.0-rc1 安装，以下命令会将它降级到 5.0.0:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 及更早版本提供了一个错误，指示已安装较新版本。

## <a name="parameters"></a>参数

|  参数 | 描述 |
| --- | --- |
| Id | 要更新的包标识符。 如果省略，则更新所有包。 -Id 开关本身是可选的。 |
| IgnoreDependencies | 跳过更新包的依赖项。 |
| ProjectName | 项目包含要更新的包，将使用默认值的所有项目的名称。 |
| 版本 | 要用于升级，默认为最新版本的版本。 NuGet 3.0 + 中的版本值必须是之一*最低、 最高、 HighestMinor*，或*HighestPatch* （等效于-安全）。 |
| 安全 | 将使用相同的主要和次要版本与当前安装的包的唯一版本升级的约束。 |
| 源 | 要搜索的程序包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Uninstall-Package`搜索当前选定的程序包源。 |
| IncludePrerelease | 包括预发行程序包更新。 |
| 重新安装 | Resintalls 使用其当前安装的版本包。 请参阅[重新安装和更新包](../consume-packages/reinstalling-and-updating-packages.md)。 |
| FileConflictAction | 当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。 可能的值为*覆盖，忽略，无、 OverwriteAll*，和*IgnoreAll* （3.0 +）。 |
| DependencyVersion | 版本的依赖项包若要使用，可以是下列项之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</li><li>*最高*（默认值为更新包不带任何参数）： 最高的版本</li></ul>你可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。 |
| ToHighestPatch | 将仅使用相同的次要版本与当前安装的包的版本升级的约束。 |
| ToHighestMinor | 将仅使用相同的主要版本与当前安装的包的版本升级的约束。 |
| WhatIf | 显示不实际执行更新运行命令时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

### <a name="common-parameters"></a>通用参数

`Update-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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