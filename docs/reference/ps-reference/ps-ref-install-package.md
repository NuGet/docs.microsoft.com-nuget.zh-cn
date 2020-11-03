---
title: NuGet Install-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Install-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237200"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Install-Package (程序包管理器控制台) 

*本主题介绍 Windows 上 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内的命令。有关通用 PowerShell Install-Package 命令，请参阅 [PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*

将包及其依赖项安装到项目中。

## <a name="syntax"></a>语法

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 + 中， `Install-Package` 可以降级项目中的现有包。 例如，如果安装了 5.1.0-rc1，以下命令会将其降级到5.0.0：

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>parameters

| 参数 | 说明 |
| --- | --- |
| ID | 需要 () 要安装的包的标识符。  ( *3.0 +* ) 该标识符可以是 `packages.config` 文件或文件的路径或 URL `.nupkg` 。 -Id 开关本身是可选的。 |
| IgnoreDependencies | 仅安装此程序包，而不安装其依赖项。 |
| 项目名称 | 要在其中安装包的项目，默认为默认项目。 |
| 源 | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。 如果省略，则 `Install-Package` 搜索当前选定的包源。 |
| 版本 | 要安装的包的版本，默认为最新版本。 |
| IncludePrerelease | 考虑安装的预发行程序包。 如果省略，则只考虑稳定程序包。 |
| FileConflictAction | 当要求覆盖或忽略项目引用的现有文件时要执行的操作。 可能的值包括 *Overwrite、Ignore、None、OverwriteAll* 和 *(3.0 +)* *IgnoreAll* 。 |
| DependencyVersion | 要使用的依赖项包的版本，可以是下列项之一：<br/><ul><li>*最低* (默认) ：最低版本</li><li>*HighestPatch* ：最小主要、次要和最高修补程序的版本</li><li>*HighestMinor* ：最小主要版本号最高的版本，最高修补程序</li><li>不带参数的 Update-Package 的 *最高* (默认值) ：最高版本</li></ul>您可以使用文件中的设置设置默认值 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` 。 |
| WhatIf | 显示运行命令时，如果不实际执行安装，会发生什么情况。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Install-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```