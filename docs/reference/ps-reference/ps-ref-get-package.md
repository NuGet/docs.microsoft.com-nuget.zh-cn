---
title: NuGet Get-Package PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中 Get-Package PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237226"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>在 Visual Studio 中 Get-Package (程序包管理器控制台) 

*本主题介绍 Windows 上 Visual Studio 中的 [包管理器控制台](../../consume-packages/install-use-packages-powershell.md) 内的命令。有关通用 PowerShell Get-Package 命令，请参阅 [PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*

检索本地存储库中安装的包的列表，列出包源中与-ListAvailable 开关一起使用时可用的包，或在与-Update 开关一起使用时列出可用的更新。

## <a name="syntax"></a>语法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

在没有参数的情况下，将 `Get-Package` 显示默认项目中安装的包的列表。

## <a name="parameters"></a>parameters

| 参数 | 说明 |
| --- | --- |
| 源 | 包的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。 如果省略，则 `Get-Package` 搜索当前选定的包源。 当与-ListAvailable 一起使用时，默认为 nuget.org。 |
| ListAvailable | 列出包源中可用的包，默认为 nuget.org。显示默认的50包，除非指定了-PageSize 和/或-First。 |
| 更新 | 列出具有包源中可用更新的包。 |
| 项目名称 | 要从中获取已安装包的项目。 如果省略，则返回整个解决方案的已安装项目。 |
| 筛选器 | 一个筛选器字符串，用于通过将包列表应用到包 ID、说明和标记来缩小包列表范围。 |
| First | 要从列表开头返回的程序包数。 如果未指定，则默认为50。 |
| 跳过 | 省略 &lt; &gt; 所显示列表中的第一个 int 包。  |
| AllVersions | 显示每个包的所有可用版本，而不是仅显示最新版本。 |
| IncludePrerelease | 在结果中包括预发布包。 |
| PageSize | *(3.0 +)* 当与-ListAvailable 一起使用时 (需要) ，并在提示继续操作之前列出要列出的包数。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Get-Package` 支持以下 [常见的 PowerShell 参数](/powershell/module/microsoft.powershell.core/about/about_commonparameters)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```