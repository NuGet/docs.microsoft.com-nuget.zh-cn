---
title: NuGet Get 包 PowerShell 参考
description: 在 Visual Studio 中的 NuGet 包管理器控制台中的 Get 包 PowerShell 命令参考。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: c70e60b7391f19026e2dcd502d667fbe1da7e6e2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>获取包 （在 Visual Studio 中的包管理器控制台）

*本主题介绍中的命令[NuGet 包管理器控制台](package-manager-console.md)Windows 上的 Visual Studio 中。泛型的 PowerShell Get 包命令，请参阅[PowerShell PackageManagement 引用](/powershell/module/packagemanagement/?view=powershell-6)。*

检索包安装在本地存储库的列表，列出从包源与-ListAvailable 开关一起使用时可用的包或列出可用的更新与-更新开关一起使用时。

## <a name="syntax"></a>语法

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

不带任何参数，`Get-Package`显示的默认项目中安装的程序包的列表。

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| 源 | 包的 URL 或文件夹路径。 本地文件夹路径可以是绝对的或相对于当前文件夹。 如果省略，`Get-Package`搜索当前选定的程序包源。 如果与-ListAvailable 一起，默认为 nuget.org。 |
| ListAvailable | 列出从包源，默认为 nuget.org 可用的包。除非指定的 PageSize 和/或-第一个，则显示默认值为 50 的包。 |
| 更新 | 列出程序包源中具有更新的包。 |
| ProjectName | 从中获取已安装的软件包项目。 如果省略，则返回安装整个解决方案的项目。 |
| 筛选器 | 用于通过将其应用到包 ID、 说明和标记缩小的包列表的筛选器字符串。 |
| First | 要从列表的开头返回的程序包数。 如果未指定，默认为 50。 |
| Skip | 省略第一个&lt;int&gt;从列表中显示的包。  |
| AllVersions | 显示每个包而不是仅最新版本的所有可用的版本。 |
| IncludePrerelease | 在结果中包含预发行程序包。 |
| PageSize | *（3.0 +)* 时与-ListAvailable 一起 （必需） 的包的数量来授予提示是否继续前列表。 |

任何这些参数接受管道输入或通配符字符。

## <a name="common-parameters"></a>通用参数

`Get-Package` 支持以下[常见的 PowerShell 参数](http://go.microsoft.com/fwlink/?LinkID=113216)： 调试、 错误操作、 ErrorVariable、 OutBuffer、 OutVariable、 PipelineVariable、 Verbose、 WarningAction 和 WarningVariable。

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
