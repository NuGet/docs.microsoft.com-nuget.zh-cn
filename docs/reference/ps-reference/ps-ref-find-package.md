---
title: NuGet 查找包 PowerShell 参考
description: Visual Studio 中的 NuGet 包管理器控制台中的 "查找包 PowerShell" 命令参考。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384628"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package （Visual Studio 中的程序包管理器控制台）

*版本 3.0 +;本主题介绍 Windows 上 Visual Studio 中的[包管理器控制台](../../consume-packages/install-use-packages-powershell.md)内的命令。对于 "通用 PowerShell 查找包" 命令，请参阅[PowerShell PackageManagement 参考](/powershell/module/packagemanagement/?view=powershell-6)。*

从包源中获取具有指定 ID 或关键字的一组远程包。

## <a name="syntax"></a>语法

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>参数

| 参数 | 描述 |
| --- | --- |
| Id &lt;关键字&gt; | 请求搜索包源时要使用的关键字。 使用-ExactMatch 仅返回其包 ID 与关键字匹配的那些包。 如果未提供任何关键字，`Find-Package` 将返回前20个包的列表（通过下载）或由-First 指定的数字。 请注意，-Id 是可选的，而不是操作。 |
| Source | 要搜索的包源的 URL 或文件夹路径。 本地文件夹路径可以是绝对路径，也可以是相对于当前文件夹的路径。 如果省略，则 `Find-Package` 搜索当前选定的包源。 |
| AllVersions | 显示每个包的所有可用版本，而不是仅显示最新版本。 |
| First | 要从列表开头返回的包数;默认值为20。 |
| Skip | 省略所显示列表中的第一个 &lt;int&gt; 包。  |
| IncludePrerelease | 在结果中包括预发布包。 |
| ExactMatch | 指定为使用 &lt;关键字&gt; 为区分大小写的包 ID。 |
| StartWith | 返回包 ID 以 &lt;关键字开头&gt;的包。 |

这些参数都不接受管道输入或通配符。

## <a name="common-parameters"></a>通用参数

`Find-Package` 支持以下[常见的 PowerShell 参数](https://go.microsoft.com/fwlink/?LinkID=113216)：调试、错误操作、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction 和 WarningVariable。

## <a name="examples"></a>示例

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
