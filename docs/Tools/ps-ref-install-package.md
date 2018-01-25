---
title: "NuGet 安装包 PowerShell 参考 |Microsoft 文档"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "在 Visual Studio 中的 NuGet 包管理器控制台的安装包 PowerShell 命令参考。"
keywords: "NuGet 包管理器控制台，NuGet Powershell 命令，NuGet Powershell 参考，安装包"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d6b0c20545ecb82b0c2fa5214508381c0279c7cd
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>安装包 （在 Visual Studio 中的包管理器控制台）

*本主题介绍中的命令[NuGet 包管理器控制台](Package-Manager-Console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell Install-package 命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

到项目中安装包及其依赖项。

## <a name="syntax"></a>语法

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

在 NuGet 2.8 +`Install-Package`将你的项目中的现有包降级。 例如，如果你有 Microsoft.AspNet.MVC 5.1.0-rc1 安装，以下命令会将它降级到 5.0.0:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

NuGet 2.7 及更早版本提供了一个错误，指示已安装较新版本。
  
## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id | （必需）要安装的包的标识符。 (*3.0 +*) 路径或 URL，该标识符可以是`packages.config`文件或`.nupkg`文件。 -Id 开关本身是可选的。 |
| IgnoreDependencies | 安装仅此包不及其依赖项。 |
| ProjectName | 要安装包，默认为默认项目到项目。 |
| 源 | 要搜索的程序包源 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Install-Package`搜索当前选定的程序包源。 |
| 版本 | 若要安装，包的版本默认为最新版本。 |
| IncludePrerelease | 将安装的预发行程序包。 如果省略，则考虑仅稳定的程序包。 |
| FileConflictAction | 当系统询问是覆盖还是忽略所引用的项目的现有文件时要执行操作。 可能的值为*覆盖，忽略，无、 OverwriteAll*，和*（3.0 +）* *IgnoreAll*。 |
| DependencyVersion | 版本的依赖项包若要使用，可以是下列项之一：<br/><ul><li>*最低*（默认值）： 最低版本</li><li>*HighestPatch*： 具有的最低主要、 越小越小、 最高的修补程序版本</li><li>*HighestMinor*： 具有最低主要版本、 最高次，最高的修补程序</li><li>*最高*（默认值为更新包不带任何参数）： 最高的版本</li></ul>你可以设置默认值使用[ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)中设置`Nuget.Config`文件。 |
| WhatIf | 显示运行命令而不实际执行安装时，会发生什么情况。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Install-Package`支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
