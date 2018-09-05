---
title: NuGet 安装包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中安装包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546021"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package （Visual Studio 中的程序包管理器控制台）

*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell 安装包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

将包及其依赖项安装到项目。

## <a name="syntax"></a>语法

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 +`Install-Package`将你的项目中的现有包降级。 例如，如果必须安装 Microsoft.AspNet.MVC 5.1.0-rc1，以下命令将降级到 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要安装的包的标识符。 (*3.0 +*) 的路径或 URL 的标识符可以是`packages.config`文件或`.nupkg`文件。 -Id 开关本身是可选的。 |
| IgnoreDependencies | 安装此包仅不及其依赖项。 |
| ProjectName | 要在其中安装包，默认值为默认项目项目。 |
| 源 | 要搜索的包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Install-Package`搜索当前所选的包源。 |
| 版本 | 若要安装，包的版本默认为最新版本。 |
| IncludePrerelease | 考虑安装的预发行包。 如果省略，则被视为仅稳定的包。 |
| FileConflictAction | 当要求您覆盖或忽略现有的项目所引用的文件时要执行的操作。 可能的值为*覆盖、 忽略、 None、 OverwriteAll*，并 *（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 版本的依赖项包使用，可以是以下值之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有最低主要、 次要最低、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最小的、 最高的修补程序</li><li>*最高*（默认值为更新包不带任何参数）： 最高版本</li></ul>您可以设置默认值使用[ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。 |
| WhatIf | 显示运行该命令而不实际执行安装时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Install-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
