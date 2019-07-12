---
title: NuGet 包获取 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中获取包 PowerShell 命令参考。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842507"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package （Visual Studio 中的程序包管理器控制台）

*本主题介绍中的命令[程序包管理器控制台](package-manager-console.md)在 Windows 上的 Visual Studio 中。有关泛型的 PowerShell Get-package 命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

检索安装在本地存储库中的包的列表，列出了与-ListAvailable 开关一起使用时的包源中可用的包或列出与-更新开关一起使用时可用的更新。

## <a name="syntax"></a>语法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

不带任何参数，`Get-Package`显示的默认项目中安装的包的列表。

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Source | 包的 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Get-Package`搜索当前所选的包源。 与-ListAvailable，一起使用时默认为 nuget.org。 |
| ListAvailable | 列出了默认值为 nuget.org 的包源中可用的包。除非另有指定的 PageSize 和/或-第一个显示默认值为 50 的包。 |
| 更新 | 列出包源中有可用更新的包。 |
| ProjectName | 获取已安装的包的项目。 如果省略，则返回安装整个解决方案的项目。 |
| 筛选器 | 用来将其应用到包 ID、 说明和标记来缩小包列表的筛选器字符串。 |
| 第一个 | 若要从列表开头返回的包数。 如果未指定，默认为 50。 |
| Skip | 省略了第一个&lt;int&gt;显示的列表中的包。  |
| AllVersions | 显示所有可用版本的每个包而不是仅最新版本。 |
| IncludePrerelease | 在结果中包括预发行包。 |
| PageSize | *（3.0 +)* 与一起使用时-ListAvailable （必需），包的数量以列出提供提示以继续之前。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Get-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216):调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable，详细、 WarningAction 和 WarningVariable。

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
